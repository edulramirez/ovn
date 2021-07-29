# ovn
Reference --> https://blog.spinhirne.com/posts/an-introduction-to-ovn/a-primer-on-ovn/

how to setup a 3 nodes OVN in centos7


centos #1 central node 192.168.122.10

#systemctl stop firewalld ; systemctl disable firewalld ;

INSTALLING OPENVSWITCH

#yum install epel-release wget openssl-devel  gcc make python-devel openssl-devel kernel-devel graphviz kernel-debug-devel autoconf automake rpm-build redhat-rpm-config libtool desktop-file-utils libcap-ng-devel groff checkpolicy selinux-policy-devel unbound unbound-devel python3-devel gcc-c++ -y

#yum install python3-sphinx -y

#useradd ovs;su - ovs

#mkdir -p ~/rpmbuild/SOURCES
#cd rpmbuild/SOURCES

#wget https://www.openvswitch.org/releases/openvswitch-2.15.0.tar.gz

#tar openvswitch-2.15.0.tar.gz

#rpmbuild -bb --nocheck openvswitch-2.15.0/rhel/openvswitch-fedora.spec

#####OUTPUT######
.
.
.

Checking for unpackaged file(s): /usr/lib/rpm/check-files /home/ovs/rpmbuild/BUILDROOT/openvswitch-2.15.0-1.el7.x86_64
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/openvswitch-2.15.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/noarch/openvswitch-selinux-policy-2.15.0-1.el7.noarch.rpm
Wrote: /home/ovs/rpmbuild/RPMS/noarch/python3-openvswitch-2.15.0-1.el7.noarch.rpm
Wrote: /home/ovs/rpmbuild/RPMS/noarch/openvswitch-test-2.15.0-1.el7.noarch.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/openvswitch-devel-2.15.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/openvswitch-ipsec-2.15.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/openvswitch-debuginfo-2.15.0-1.el7.x86_64.rpm
Executing(%clean): /bin/sh -e /var/tmp/rpm-tmp.JOgAQ3
+ umask 022
+ cd /home/ovs/rpmbuild/BUILD
+ cd openvswitch-2.15.0
+ rm -rf /home/ovs/rpmbuild/BUILDROOT/openvswitch-2.15.0-1.el7.x86_64
+ exit 0

===> as root

#yum localinstall /home/ovs/rpmbuild/RPMS/x86_64/openvswitch-2.15.0-1.el7.x86_64.rpm

#systemctl start openvswitch.service
#systemctl enable openvswitch.service
#systemctl status openvswitch.service

INSTALLING OVN

#su - ovs

#cd rpmbuild/SOURCES/

#wget https://github.com/ovn-org/ovn/archive/refs/tags/v21.03.0.tar.gz

#mv v21.03.0.tar.gz ovn-21.03.0.tar.gz
#tar zxf ovn-21.03.0.tar.gz

#sed -e 's/@OVSVERSION@/2.15.0/' ovn-21.03.0/rhel/ovn-fedora.spec.in > /tmp/ovs.spec
#sed -i 's/@VERSION@/21.03.0/'  /tmp/ovs.spec
#sed -i 's/sphinx-build/sphinx-build-3/g' /tmp/ovs.spec

#rpmbuild -bb --nocheck /tmp/ovs.spec


####OUTPUT

Checking for unpackaged file(s): /usr/lib/rpm/check-files /home/ovs/rpmbuild/BUILDROOT/ovn-21.03.0-1.el7.x86_64
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/ovn-21.03.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/ovn-central-21.03.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/ovn-host-21.03.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/ovn-vtep-21.03.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/ovn-docker-21.03.0-1.el7.x86_64.rpm
Wrote: /home/ovs/rpmbuild/RPMS/x86_64/ovn-debuginfo-21.03.0-1.el7.x86_64.rpm
Executing(%clean): /bin/sh -e /var/tmp/rpm-tmp.3PrTjO
+ umask 022
+ cd /home/ovs/rpmbuild/BUILD
+ cd ovn-21.03.0
+ rm -rf /home/ovs/rpmbuild/BUILDROOT/ovn-21.03.0-1.el7.x86_64
+ exit 0



==> As root

#yum localinstall /home/ovs/rpmbuild/RPMS/x86_64/ovn-21.03.0-1.el7.x86_64.rpm
#yum localinstall /home/ovs/rpmbuild/RPMS/x86_64/ovn-central-21.03.0-1.el7.x86_64.rpm



in hosts
yum localinstall /home/ovs/rpmbuild/RPMS/x86_64/ovn-21.03.0-1.el7.x86_64.rpm






















