clean:
	rm ca-*
	rm cert-*
	rm index.*
	rm serial.*
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

kafka.server.keystore.jks:
	keytool -keystore kafka.server.keystore.jks \
    	  -alias localhost \
    	  -validity 365 \
    	  -genkey \
    	  -keyalg RSA \
    	  -deststoretype pkcs12 \
    	  -dname 'CN=my-server,OU=Consulting,O=redhat.com,L=Rome,S=RM,C=IT' \
    	  -ext SAN=DNS:localhost,IP:127.0.0.1 \
    	  -storepass changeit

cert-file: kafka.server.keystore.jks
	keytool -keystore kafka.server.keystore.jks \
    	  -alias localhost \
    	  -certreq \
    	  -file cert-file \
    	  -ext SAN=DNS:localhost,IP:127.0.0.1 \
    	  -storepass changeit

cert-signed: cert-file
	openssl ca -config openssl-ca.cnf \
    	  -policy signing_policy \
    	  -extensions signing_req \
    	  -out cert-signed -batch \
    	  -infiles cert-file

kafka.client.truststore.jks: ca-cert
	keytool -keystore kafka.client.truststore.jks \
    	  -alias CARoot \
    	  -importcert \
    	  -file ca-cert \
    	  -storepass changeit \
    	  -noprompt

kafka.server.truststore.jks: ca-cert
	keytool -keystore kafka.server.truststore.jks \
    	  -alias CARoot \
    	  -importcert \
    	  -file ca-cert \
    	  -storepass changeit \
    	  -noprompt

import: ca-cert cert-signed
	keytool -keystore kafka.server.keystore.jks \
    	  -alias CARoot \
    	  -importcert \
    	  -file ca-cert \
    	  -storepass changeit \
    	  -noprompt

	keytool -keystore kafka.server.keystore.jks \
    	  -alias localhost \
    	  -importcert \
    	  -file cert-signed \
    	  -storepass changeit \
    	  -noprompt

all: import kafka.server.truststore.jks kafka.client.truststore.jks
