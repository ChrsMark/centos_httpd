# centos_httpd

This repo can be used to serve your `.rpm` packages.

- `docker build -t yum-repo-server .`
- `docker-compose up -d`

Move your `mypack-2.0-1.el7.x86_64.rpm` file under `/rpm_packages`


You can now wget your `mypack-2.0-1.el7.x86_64.rpm` file with: `wget http://IP:8009` and install it on your CentOS machine.

Otherwise you can setup a yum repo inside the continer with `docker exec -it yum-repo-server createrepo /var/www/html`

Now on a client CentOS machine:

```
cat << EOF > /etc/yum.repos.d/mypack.repo
  [remote]
  name=RHEL Apache
  baseurl=http://IP:8009
  enabled=1
  gpgcheck=0
EOF
```
Then `yum install mypack`
