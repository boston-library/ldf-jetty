# ldp-jetty

This is a copy of jetty with the needed applications for running Linked Data Fragments.  These include two java-based applications:

* [Blazegraph](https://wiki.blazegraph.com/wiki/index.php/NanoSparqlServer)
* [Marmotta](http://marmotta.apache.org/)

## Included Versions

* Jetty: 8.1.16
* Blazegraph: 2.0.1
* Marmotta: 3.3.0

## Usage

### Dependencies

* [Java 8 (JRE)](https://java.com/en/download/index.jsp)

### Manual

    git clone https://github.com/boston-library/ldp-jetty.git
    cd  ldp-jetty
    java -Xmx2048m -jar start.jar

You can also change the port jetty starts on by editing the file etc/jetty.xml and changing this line to indicate a different port number:

    <Set name="port"><SystemProperty name="jetty.port" default="8988"/></Set>

It is recommended that you populate Blazegraph with LoC for terms to work. To do this:

* Download the latest subjects vocab from: [http://id.loc.gov/download/](http://id.loc.gov/download/) (the nt version of “LC Subject Headings (SKOS/RDF only)”)

* Extract the above download into a directory.

* Run the following command from that extraction directory:
    curl -H 'Content-Type: text/turtle' --upload-file subjects-skos-20140306.nt -X POST "http://localhost:8988/blazegraph/sparql?context-uri=http://id.loc.gov/static/data/authoritiessubjects.nt.skos.zip"

### Using ldfwrapper

For use within your application's Rails directory.

    add 'ldf-wrapper' to your gemfile

Download and install the instance:

    $ rake ldfjetty:install

Whenever you want to start it up, do:

    $ rake ldfjetty:start

Shut it down with:

    $ rake ldfjetty:stop

To reinstall a fresh copy, you can either remove the "ldf-jetty" directory or do "rake jetty:clean" and then rerun:

    $ rake ldfjetty:install

See [ldfwrapper](https://github.com/boston-library/ldf-wrapper) for more information regarding configuration and usage.
Port numbers and other java options maybe configured via the gem.

### Interaction

When jetty is finished initializing itself, Blazegraph is available at

* [http://localhost:8988/blazegraph/](http://localhost:8988/blazegraph/)

and Marmotta is available at

* [http://localhost:8988/marmotta/](http://localhost:8988/marmotta/)

You can see a list of all installed applications at

* [http://localhost:8988](http://localhost:8988)

