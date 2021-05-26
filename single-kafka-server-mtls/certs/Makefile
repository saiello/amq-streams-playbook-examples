clean:
	rm index.*
	rm serial.*
	rm ca-*
	rm *-file
	rm *-signed
	rm *.jks
	rm *.pem

serial.txt:
	echo 01 > serial.txt

index.txt:
	touch index.txt

ca-cert: serial.txt index.txt
	openssl req -x509 \
	  -config openssl-ca.cnf \
    	  -newkey rsa:4096 \
    	  -sha256 \
    	  -nodes \
    	  -keyout ca-key \
    	  -out ca-cert \
    	  -outform PEM \
    	  -subj '/C=IT/ST=RM/L=Rome/O=redhat.com/OU=Consulting/CN=my-ca/'

%.truststore.jks:
	keytool -keystore $*.truststore.jks \
    	  -alias CARoot \
    	  -importcert \
    	  -file ca-cert \
    	  -storepass changeit \
    	  -noprompt


%.keystore.jks:
	keytool -keystore $*.keystore.jks \
    	  -alias localhost \
    	  -validity 365 \
    	  -genkey \
    	  -keyalg RSA \
    	  -deststoretype pkcs12 \
    	  -dname 'CN=my-$*,OU=Consulting,O=redhat.com,L=Rome,S=RM,C=IT' \
    	  -ext SAN=DNS:localhost,IP:127.0.0.1 \
    	  -storepass changeit

	keytool -keystore $*.keystore.jks \
    	  -alias localhost \
    	  -certreq \
    	  -file $*-file \
    	  -ext SAN=DNS:localhost,IP:127.0.0.1 \
    	  -storepass changeit

	openssl ca -config openssl-ca.cnf \
    	  -policy signing_policy \
    	  -extensions signing_req \
    	  -out $*-signed -batch \
    	  -infiles $*-file

	keytool -keystore $*.keystore.jks \
    	  -alias CARoot \
    	  -importcert \
    	  -file ca-cert \
    	  -storepass changeit \
    	  -noprompt

	keytool -keystore $*.keystore.jks \
    	  -alias localhost \
    	  -importcert \
    	  -file $*-signed \
    	  -storepass changeit \
    	  -noprompt

all: kafka.server.keystore.jks kafka.server.truststore.jks kafka.client.keystore.jks kafka.client.truststore.jks
