## How to build the website

```
mkdocs serve      -f web-mkdocs.yml
mkdocs gh-deploy  -f web-mkdocs.yml
```

## How to build the PDF document

```
git clone https://github.com/ebadi/mkdocs-with-pdf
cd mkdocs-with-pdf
git checkout docker-fix

export GOKARTDOC=/home/wave/GoKart/gokart-documentation
export GOKARTDOC=/home/hamid/repositories/gokart-documentation/

cd docker/mkdocs-with-pdf
mkdir ./docs-src/
sudo mount --bind   $GOKARTDOC  ./docs-src/
docker-compose build
docker-compose run debian build
```

Output:


```
INFO     -  Found PDF rendering event hook module.
INFO     -  Cleaning site directory
INFO     -  Building documentation to directory: /docs/site
INFO     -  The following pages exist in the docs directory, but are not included in the "nav" configuration:
              - missing.md
INFO     -  [SASS] Build CSS "assets/stylesheets/extra-style.7ci1ioua.min.css" from "extra_sass/style.css.scss"
INFO     -  (hook on inject_link: Home)
INFO     -  (hook on inject_link: High Level Architecture)
INFO     -  (hook on inject_link: Autonomous Drive)
INFO     -  (hook on inject_link: Body Electronics)
INFO     -  (hook on inject_link: HW and Board Components)
INFO     -  (hook on inject_link: Contact Infotiv)
INFO     -  (hook on inject_link: For Developers)
INFO     -  (hook on inject_link: Interfaces and Sensors)
INFO     -  (hook on inject_link: Common Issues)
INFO     -  (hook on inject_link: Missing)
INFO     -  (hook on inject_link: Automotive Platform)
INFO     -  (hook on inject_link: Software Repositories)
INFO     -  (hook on inject_link: Start the GoKart)
INFO     -  (hook on inject_link: Glossary of Terms)
INFO     -  Number headings up to level 3.
INFO     -  Generate a table of contents up to heading level 3.
INFO     -  Generate a cover page with "default_cover.html.j2".
INFO     -  Generate a back cover page with "default_back_cover.html.j2".
ERROR    -  Failed to generate the back cover page: No filter named 'qrcode' found.
INFO     -  Converting <img> alignment(workaround).
INFO     -  Converting <iframe> to poster image(if available).
INFO     -  Converting for two-column layout(heading level 3).
INFO     -  Rendering on `Headless Chrome`(execute JS).
[0706/105008.644654:ERROR:bus.cc(398)] Failed to connect to the bus: Failed to connect to socket /run/dbus/system_bus_socket: No such file or directory
[0706/105008.644702:ERROR:bus.cc(398)] Failed to connect to the bus: Failed to connect to socket /run/dbus/system_bus_socket: No such file or directory
[0706/105008.645552:WARNING:bluez_dbus_manager.cc(247)] Floss manager not present, cannot set Floss enable/disable.
[0706/105008.654764:WARNING:sandbox_linux.cc(376)] InitializeSandbox() called with multiple threads in process gpu-process.
INFO     -  Rendering for PDF.
INFO     -  Output a PDF to "/docs/site/../infotiv-gokart.pdf".
GSUB/GPOS Coverage is not sorted by glyph ids.
GSUB/GPOS Coverage is not sorted by glyph ids.
INFO     -  Converting 14 articles to PDF took 6.0s
INFO     -  Documentation built in 7.17 seconds

```




