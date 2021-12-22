# default-attributes_xsd_Problem

We use Saxon  10.5EE (java) for XSLT transformations, called from command-line which works perfectly as expected:
```
java  -cp %saxon% ^
com.saxonica.Transform -val:lax -o:out.xml -s:xml/T0_Doc.xml -xsl:xsl/transT0.xsl
```
We use ```-val:lax``` because we want to expand the default-attributes. 

For differents reasons, we need to move the „-val“-Option  to a saxon config-file:
```
java  -cp %saxon% ^
com.saxonica.Transform -config:saxonConfig/config.xml -o:out.xml -s:xml/T0_Doc.xml -xsl:xsl/transT0.xsl
```

Now I get the following error:
„Cannot use a schema-validated source document unless the stylesheet is schema-aware“

We can't use schema-aware transformation, beacuse we use a lot huge XSLT's, whichs raises type-errors when using schema-aware transformation and we can't rewrite them.
Our requirements in this case are:
- expand the default-attributes
- no schema-aware transformation
- use saxon config-file for commandline options

The command-line option ```-val:lax``` does exactly what we want to do, but we need this option set in config-file without raising the metioned error
Is there a difference between ```-val:lax``` and ```<global schemaValidation="lax"/>```?

