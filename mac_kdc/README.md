# Running KDC on MAC

## Remove old volume:
 docker volume rm alluxio-secure-hadoop_keystore
 docker volume rm alluxio-secure-hadoop_keytabs
 docker volume rm alluxio-secure-hadoop_kdc_storage


## Start the KDC container
 docker-compose up -d


## Add principle:
kadmin -p admin/admin -w admin -q "xst -k alluxio.keytab alluxio/localhost@EXAMPLE.COM"

kadmin -p admin/admin -w admin -q "addprinc -pw admin alluxio/localhost@EXAMPLE.COM"


## Create a file "/etc/krb5.conf" on the MAC:
[logging]
 default = FILE:/var/log/kerberos/krb5libs.log
 kdc = FILE:/var/log/kerberos/krb5kdc.log
 admin_server = FILE:/var/log/kerberos/kadmind.log

[libdefaults]
 default_realm = EXAMPLE.COM
 dns_lookup_realm = false
 dns_lookup_kdc = false
 ticket_lifetime = 24h
 renew_lifetime = 7d
 forwardable = true

[realms]
 EXAMPLE.COM = {
  #kdc = tcp/kdc.kerberos.com:88
  #admin_server = tcp/kdc.kerberos.com:88
  kdc = kdc.kerberos.com:88
  admin_server = kdc.kerberos.com:88
 }

[domain_realm]
 .kdc.kerberos.com = EXAMPLE.COM
 kdc.kerberos.com = EXAMPLE.COM

## Create a TLS keystore and truststore
keytool -genkeypair -alias key -keyalg RSA -keysize 2048 -dname "cn=localhost, ou=Department, o=Company, l=City, st=State, c=US" -ext "SAN=ip:192.168.31.14,ip:192.168.3.28" -keystore ./keystore.jks -keypass keypass -storepass storepass

keytool -export -alias key -keystore keystore.jks -storepass storepass -rfc -file selfsigned.cer

keytool -import -alias key -noprompt -file selfsigned.cer -keystore truststore.jks -storepass trustpass

## Stop the KDC container
 docker-compose down
