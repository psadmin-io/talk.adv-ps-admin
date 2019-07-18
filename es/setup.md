# Setup for Demos

> On a fresh Linux PI installation

## Set OS Settings

```bash
sudo sysctl -w vm.max_map_count=262144
```

## psadmin_plus

```bash
sudo /opt/puppetlabs/puppet/bin/gem install psadmin_plus
echo 'PATH=$PATH:/opt/puppetlabs/puppet/bin' >> ~/.bashrc
```

## Download getMOSPatch

```bash
sudo su - psadm1
curl -L https://github.com/MarisElsins/getMOSPatch/raw/master/getMOSPatch.jar -o getMOSPatch.jar
```

## Install Elasticsearch

```bash
JAVA_HOME=/u01/app/oracle/product/pt/jdk1.8.0_191
PATH=$PATH:$JAVA_HOME/bin
java -jar getMOSPatch.jar patch=29589421 download=all platform=226P MOSUser=dan@psadmin.io MOSPass=<pass>
unzip ESK*.zip

# ##########
# Silent Install still not quite right
# The encrypt utility does not provide a {V2.1} key, but it
# will write it to an existing esuers.yml file.
# Not friendly for scripting an initial installation
# ##########

# cd archives
# tar xvf pt-elasticsearch-*.tgz
# ES_HOME=`pwd`
# PLUGIN_CLASSPATH="$ES_HOME/plugins/orcl-security-plugin/*"
# PLUGIN_CLASSPATH="$PLUGIN_CLASSPATH:$ES_HOME/lib/*"
# PASSWORD="Passw0rd"
# java -Dplugin.path.home="$ES_HOME/plugins/orcl-security-plugin" -Des.path.home="$ES_HOME/plugins/orcl-security-plugin" -cp "$PLUGIN_CLASSPATH"  com.peoplesoft.pt.elasticsearch.pscipherwrapper.PSESUser addusersilent esadmin2 "$PASSWORD" admin,read,security

cd ../setup
# vi silentInstall.config
# Add parameters and the encryption password
# ./psft-dpk-setup.sh --install_silent --install_base_dir /u01/app/oracle/product/pt/es --config_file silentinstall.config

./psft-dpk-setup.sh --install --install_base_dir /u01/app/oracle/product/pt/es 
# Passwords: Passw0rd
# Min Nodes: 2
# Install Kibana: n
# Discovery Hosts: ["127.0.0.1", "[::1]", "10.0.1.2"]
# Install Kibana: y
# Hostname: http://hr030-lnxft-1.midtier.psft.oraclevcn.com
cat /u01/app/oracle/product/pt/es/pt/elasticsearch6.1.2/plugins/orcl-security-plugin/config/properties/esusers.yml
# Grab the encrypted passwords to re-use for nodes 2/3
# esadmin: "{V2.1}v26upR1zUWTQ1NvsEwbM6pfolWr/nXee"
# people: "{V2.1}v26upR1zUWTQ1NvsEwbM6pfolWr/nXee"

cp silentinstall.config silentinstall2.config
vi silentinstall2.config
# Install elasticsearch?[Y/N]= y
# network.host= <hostname>
# http.port= 9210
# discovery.zen.ping.unicast.hosts= ["127.0.0.1", "[::1]", "10.0.1.2"]
# minimum_master_nodes= 2
# ES_HEAP_SIZE= 1
# esadmin.password= {V2.1}v26upR1zUWTQ1NvsEwbM6pfolWr/nXee
# people.password= {V2.1}v26upR1zUWTQ1NvsEwbM6pfolWr/nXee
# Install kibana?[Y/N]= n
./psft-dpk-setup.sh --install_silent --install_base_dir /u01/app/oracle/product/pt/es2 --config_file silentinstall2.config

cp silentinstall2.config silentinstall3.config
vi silentinstall3.config
# http.port= 9220
./psft-dpk-setup.sh --install_silent --install_base_dir /u01/app/oracle/product/pt/es3 --config_file silentinstall3.config

# To start ES after a config change
nohup bin/elasticsearch &

# To find a specific ES node
ps -ef | grep elastic | grep es2

# Open Firewall Ports
sudo iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 9200 -s 0.0.0.0/0 -j ACCEPT
sudo iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 9210 -s 0.0.0.0/0 -j ACCEPT
sudo iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 9220 -s 0.0.0.0/0 -j ACCEPT
sudo iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 5601 -s 0.0.0.0/0 -j ACCEPT
```

## Install mitmproxy

```bash
curl -L https://snapshots.mitmproxy.org/4.0.4/mitmproxy-4.0.4-linux.tar.gz -o mitmproxy.tar.gz
tar xvf mitmproxy.tar.gz

```

## Install Cerebtro

```bash
curl -L https://github.com/lmenezes/cerebro/releases/download/v0.8.3/cerebro-0.8.3.tgz -o cerebro.tgz
tar xvf cerebro.tgz
cd cerebro-0.8.3
vi conf/application.conf
# Add config/pass for the local cluster
JAVA_HOME=/u01/app/oracle/product/pt/jdk1.8.0_191
PATH=$PATH:$JAVA_HOME/bin
nohup bin/cerebro &
```


## psft.sh Wrapper

```bash
sudo su - psadm2
curl -L https://gist.githubusercontent.com/iversond/f9410411d10049a805353ea65d99a690/raw/cff0181619a3291d913199e5491663f5a8742bd3/psft.sh -o psft.sh
chmod +x psft.sh
curl -L https://gist.githubusercontent.com/iversond/8dc2adf8373737ad92c8c98e7f901568/raw/3f943b5e07fc13fc677f499d8f8a22ba9745d8d5/shell_sample.sh -o shell_sample.sh
chmod +x shell_sample.sh
# /u01/app/oracle/product/home/psadm2/psft.sh
# /u01/app/oracle/product/home/psadm2/shell_sample.sh
```

## IO Fluid Stylesheets

Download the DMW project and stage it on the server.

```bash
sudo su - psadm2
cd $PS_CFG_HOME
mkdir -p dmw/styles
cd dmw/styles
curl -L https://github.com/psadmin-io/io-styles-fluid/releases/download/1.0.1/IO_STYLES_FLUID.zip -o IO_STYLES_FLUID.zip
unzip IO_STYLES_FLUID.zip
exit
```

Create the DMW File Location.

```bash
sudo su - oracle2
. oraenv
#ORACLE_SID = [] ? CDBFSCM
#ORACLE_HOME = [] ? /u01/app/oracle/product/db/oracle-server/12.1.0.2
sqlplus / as sysdba
SQL> alter session set container=EPPUM;

```