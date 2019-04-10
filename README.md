# dpkg-buildpack

Sample buildpack that installs debian files found in a directory called `debs` in your application root.

For example to install the debian file for socat, place it in `debs/` in the app directory for a simple staticfile app. Then you can install with the following manifest:

```yaml
applications:
- name: myapp
  buildpacks:
  - https://github.com/smarsh/dpkg-buildpack
  - https://github.com/cloudfoundry/apt-buildpack
  - staticfile_buildpack
  disk_quota: 1G
  instances: 1
  memory: 64M
  random-route: true
  stack: cflinuxfs3
```

with the following in apt.yml as dependencies for socat:

```yaml
packages:
- libssl1.1
- libc6
- libwrap0
```

In the final app socat will be available in `/home/vcap/deps/usr/bin/socat` which is on the PATH for the running application

There are no tests.
