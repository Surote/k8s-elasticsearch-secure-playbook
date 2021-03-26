# Generate signed key pair
$ openssl genrsa -out ca.key 2048

# Create a self signed Certificate, valid for 10yrs with the 'signing' option set
$ openssl req -x509 -new -nodes -key ca.key -subj "/CN=${COMMON_NAME}" -days 3650 -reqexts v3_req -extensions v3_ca -out ca.crt

# Create secret for CA key pair
# kubectl create secret tls ca-key-pair --cert=ca.crt --key=ca.key -n elastic

# Create issuer CA
# kubectl apply -f selfsigned_issuer_ca.yml -n elastic

# Issue Certificate to secret
# kubectl apply -f create_certificate.yml -n elastic

# The result will be in secret
# kubectl get secret -n elastic
# you will see elasticsearch-ca. It include ca.crt, tls.crt,tls.key all for certificate
