# osc14_how_to_write_openqa_tests
Here you can find needles and tests source file to follow [osc14 openqa talk](https://www.youtube.com/watch?v=EM3XmaQXcLg)

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
