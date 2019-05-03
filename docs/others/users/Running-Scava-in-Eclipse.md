
# Running Scava in Eclipse

This page gives **general guidelines for running Ossmeter platform in Eclipse**

The screeshot below will be used as a reference :

<a href="http://ibb.co/mRUAVm"><img src="http://preview.ibb.co/fty4qm/eclipse_Product.png" alt="eclipse Product" border="0" /></a>

(Eclipse version used in screenshot : Eclipse Java EE IDE for Web developers Luna 2 (4.4.2) )

1. We compile with `Ossmeterfromfeature.product` file in `org.ossmeter.platform.osgi` (highlighted above)
2. In the file we put program arguements : `-apiServer`, `-master`, `-slave`. More information on https://github.com/crossminer/crossminer/wiki/Running-the-platform
3. We must validate with the button on corner top right (highlighted above). This will add the required packages.
4. If the required packages are still missing, go to `Run Configurations -> Plug-ins` and click on `Add Required Plugins`.

<a href="http://ibb.co/fjC5Vm"><img src="http://preview.ibb.co/gHoeqm/Eclipse2.jpg" alt="Eclipse2" border="0" /></a>

5. You could also check the `general information`, if its the same (as in the screenshot below).

<a href="http://ibb.co/mk89O6"><img src="http://preview.ibb.co/n2JnAm/Eclipse_Overview.png" alt="Eclipse Overview" border="0" /></a>

These were some of the things for running the platform. If there is any issue still, do not hesitate to contact us.
