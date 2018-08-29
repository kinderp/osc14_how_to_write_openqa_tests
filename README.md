# osc14_how_to_write_openqa_tests
Here you can find needles and tests source file to follow [osc14 openqa talk](https://www.youtube.com/watch?v=EM3XmaQXcLg)

## Installation [origin](https://github.com/os-autoinst/openQA/blob/master/docs/Installing.asciidoc)

* Install openQA

`sudo zypper in openQA`

* Copy apache template setup for openQA

`sudo cp /etc/apache2/vhosts.d/openqa.conf.template /etc/apache2/vhosts.d/openqa.conf`

* Enalbe some apache modules
`
a2enmod headers
a2enmod proxy
a2enmod proxy_http
a2enmod proxy_wstunnel
`

* Disable https in /etc/openqa/openqa.ini (you just can set httpsonly field to zero).
```
[openid]
## base url for openid provider
#provider = https://www.opensuse.org/openid/user/
## enforce redirect back to https
httpsonly = 0
```

* Run all your services
```
systemctl start postgresql
systemctl start openqa-gru
systemctl start openqa-webui
systemctl restart apache2
```

* Log in openqa http://localhost and create your key and secret (see the video for a clear explanation)

* Set your key and secret in `/etc/openqa/client.conf`

```
[localhost]
key = E5A393F0247EB73A
secret = 58C2D16DDF23BAEC
```

* Install the worker

`sudo zypper in openQA-worker`

* Copy auth file for your client (if openqa dir does not exist feel free to create it).

`sudo cp /etc/openqa/client.conf $HOME/.config/openqa/client.conf`



## Get the needles
- 1 `cd /var/lib/openqa/tests`
- 2 `sudo git clone https://github.com/kinderp/osc14_how_to_write_openqa_tests.git slitaz-4`
- 3 `chown -R geekotest:www slitaz-4`
- 4 `cd /var/lib/openqa/factory/iso`
- 5 `aria2c http://mirror1.slitaz.org/iso/4.0/slitaz-4.0.iso`
- 6 `chown geekotest:root slitaz-4.0.iso`
- 7 submit your job with the following command

```
/usr/share/openqa/script/client jobs post \
DISTRI=slitaz-4 VERSION=4.0 ARCH=i586 \
TEST=foo MACHINE=bar NICMODEL=e1000 \
DESKTOP=default ISO=slitaz-4.0.iso
```

## Launch the worker and see what happens in webui

`sudo systemctl openqa-worker@1`
