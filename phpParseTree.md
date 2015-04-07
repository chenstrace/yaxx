# Introduction #
The Parse\_Tree extension generates an XML parse tree from a php source code. For example:
```
<?php
if (!extension_loaded('parse_tree')) {
$prefix = (PHP_SHLIB_SUFFIX === 'dll') ? 'php_' : '';
dl($prefix . 'parse_tree.' . PHP_SHLIB_SUFFIX);
}
echo generate_parse_tree(__FILE__);
?>
```
Will output something very ugly like:
```
<yaxx:T_IF id="4">if</yaxx:T_IF>
<yaxx:CHAR40 id="6">(</yaxx:CHAR40>
<yaxx:expr id="28">
<yaxx:expr_without_variable id="27">
<yaxx:CHAR33 id="8">!</yaxx:CHAR33>
<yaxx:expr id="24">
<yaxx:r_variable id="23">
<yaxx:variable id="20">
<yaxx:base_variable_with_function_calls id="1d">
<yaxx:function_call id="1c">
<yaxx:T_STRING id="a">extension_loaded</yaxx:T_STRING>
<yaxx:CHAR40 id="c">(</yaxx:CHAR40>
etc...
```
This extension also provides an XSLT stylesheet able to output a php source code from an
XML parse tree.
```
define('XML_OPTIONS', LIBXML_DTDLOAD | LIBXML_NOENT | LIBXML_DTDATTR | LIBXML_NOCDATA);
 
$source = parse_tree_from_file('source/order.php');
/*
Tree modifications...
*/
$xml = new DOMDocument;
$xml->loadXML($source, XML_OPTIONS);
 
$xsl = new DOMDocument;
$xsl->load('toWrite.xsl', XML_OPTIONS);
 
$proc = new XSLTProcessor;
$proc->importStyleSheet($xsl);
file_put_contents('target/order.php', $proc->transformToXML($xml));
```
So now you just have to create your own XSLT stylesheet to perform any operations you want
(code optimization, code obfuscation, whatever...).

# The parse tree generator #
If you want, you can try this extension without installing it: http://phpaspect.org/ast

# Contacts #
You can join the googlegroups about this pecl extension:
[php\_parse\_tree@googlegroups.com](mailto:php_parse_tree@googlegroups.com),
[see the archives](http://groups-beta.google.com/group/php_parse_tree).

If you have any specific question, you can e-mail me directly:
[wcandillon@elv.telecom-lille1.eu](mailto:wcandillon@elv.telecom-lille1.eu).