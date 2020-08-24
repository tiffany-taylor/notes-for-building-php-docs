# Notes for building PHP docs from php-docs VM
`ssh tiffany@10.0.37.151` to log into VM  
TODO: change IP address to `10.11.0.something`

may need to remount doc-en in VM if folder is empty on VM  
`sudo mount -t vboxsf doc-en ~/php-docs/doc-en`

two folders in Windows, one is a github clone (`D:\projects\php\doc-en`) and the other is a shared folder with VM (`D:\projects\php\php-docs`)

processes  
if making a PR with Github:  
- modify files in `doc-en`, copy file to the shared folder with VM, then run configuration

if committing directly to SVN:
- modify files inside `php-docs` directly, run configuration

`rendered-docs-xhtml` is another shared folder where the rendered docs are output into and can be viewed in a web browser on host machine without loading a web server (kind of avoids broken link issue with built-in PHP web server that is a pervasive problem...)
`rendered-docs-xhtml` may also need to be remounted...  
`sudo mount -t vboxsf rendered-docs-xhtml ~/rendered-docs-xhtml`

to configure:
```
cd ~
php ~/php-docs/doc-en/doc-base/configure.php --enable-xml-details --disable-segfault-error
```

to render:
```
cd ~
php ~/php-docs/phd/render.php --docbook ~/php-docs/doc-en/doc-base/.manual.xml --package PHP --format xhtml --output rendered-docs-xhtml
```

other notes:
* http://doc.php.net/tutorial/local-setup.php
* https://www.sammyk.me/how-to-contribute-to-php-documentation
* https://github.com/php/web-php/blob/master/README.md
