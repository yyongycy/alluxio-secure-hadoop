# Alluxio config for Dora and Kerberos
```

alluxio.network.tls.enabled=true
alluxio.network.tls.keystore.path=/opt/alluxio/keystore.jks
alluxio.network.tls.keystore.alias=key
alluxio.network.tls.keystore.password=storepass
alluxio.network.tls.keystore.key.password=keypass
# truststore properties for the client side of connections (worker to master, or master to master for embedded journal)
alluxio.network.tls.truststore.path=/opt/alluxio/truststore.jks
alluxio.network.tls.truststore.password=trustpass
alluxio.network.tls.server.protocols=TLSv1.2

alluxio.security.authentication.type=KERBEROS
alluxio.security.authorization.permission.enabled=true
alluxio.security.kerberos.unified.instance.name=localhost
alluxio.security.kerberos.server.principal=alluxio/localhost@EXAMPLE.COM
alluxio.security.kerberos.server.keytab.file=/etc/security/keytabs/alluxio.keytab
alluxio.security.kerberos.client.principal=alluxio/localhost@EXAMPLE.COM
alluxio.security.kerberos.client.keytab.file=/etc/security/keytabs/alluxio.keytab
alluxio.security.kerberos.auth.to.local=RULE:[1:$1@$0](alluxio.*@.*EXAMPLE.COM)s/.*/alluxio/ RULE:[1:$1@$0](A.*@EXAMPLE.COM)s/A([0-9]*)@.*/a$1/ DEFAULT
alluxio.master.security.impersonation.root.users=*
alluxio.master.security.impersonation.rm.users=*
alluxio.master.security.impersonation.nm.users=*
alluxio.master.security.impersonation.yarn.users=*
alluxio.master.security.impersonation.hive.users=*


alluxio.dora.client.read.location.policy.enabled=true
alluxio.user.short.circuit.enabled=false
alluxio.master.worker.register.lease.enabled=false
alluxio.dora.client.ufs.root=/tmp/alluxio
alluxio.worker.block.store.type=PAGE
alluxio.worker.page.store.type=LOCAL
alluxio.worker.page.store.dirs=/Volumes/ramdisk
alluxio.worker.page.store.sizes=1GB
alluxio.worker.page.store.page.size=1MB

alluxio.master.backup.directory=/tmp/alluxio_backups
alluxio.standby.master.web.enabled=false
```
