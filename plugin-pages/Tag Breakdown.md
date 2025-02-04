
Tags similar to these should appear as a direct

<BODY>

descendant on merchant product page with a successful MasterTag
integration. The parameter values will defer per integration

## MyThings


``` html4strict

<script type="text/javascript" id="_aw_script_0" src="http://rainbowx.mythings.com/c.aspx?atok=awin-2650-100-uk"></script>
```


## Next Performance


``` html4strict

<script type="text/javascript" id="_aw_script_0" src="http://nxtck.com/act.php?zid=21950&pid=397921"></script>
zid = product zone ID
```


## Criteo


``` html4strict


<div id="pcto_dis_div" style="display: none; ">
<iframe width="1px" height="1px" style="" src="http://dis.criteo.com/dis/dis.aspx?c=2&p=2305&cb=74130876408"></iframe></div>
```


## Struq


``` html4strict

<iframe src="http://app.struq.com/s/s/[PRODUCTDETAILSTOKEN]/?v=2&rnd=1234567890&sl_ctx=detail&sl_pid=ABC123" width="1" height="1" frameborder="0" marginheight="0" marginwidth="0" scrolling="no" style="position:absolute"></iframe>
```


## AdGENIE


``` html4strict

<img src="https://adverts.adgenie.co.uk/genieTracker.php?adgCompanyID=wgFGaaEGuzyxtcCmcopd&adgItem=PRODUCT_ID" alt="" width="1" />
<img src="http://ib.adnxs.com/seg?add=95298&t=2" width="1" height="1" />
```


## Ve Interactive


``` html4strict

<script type="text/javascript" id="_aw_script_0" src="http://config1.veinteractive.com/vecapturev5.js"></script>
```


## Merchenta


``` html4strict

<div id="mc_data" style="display: none; "><div class="mc_retailer">awinTest</div>
   <div class="mc_event">VIEW</div>
   <div class="mc_sku">256461</div>

<script type="text/javascript" id="_aw_script_0" src="http://cdn.merchenta.com/track/t.js"></script>
```


## Criteo Tag Surgery

Just in case you get the complete tag from the behavioural retargeter
instead of the prerequisite parameters. You can still fish them out of
the code:


``` html4strict

Product page:

<script type="text/javascript">
function pcto_dis()
{
if (document.createElement) { var cto_dis_im=document.createElement('IFRAME');if (cto_dis_im) { cto_dis_im.width = '1px'; cto_dis_im.height = '1px'; cto_dis_im.style.display='none'; cto_dis_im.src='http://dis.criteo.com/dis/dis.aspx?c=2&p=2305&cb='+Math.floor(Math.random()*99999999999); var cto_dis_doc=document.getElementById('pcto_dis_div'); if (cto_dis_doc!==null && cto_dis_doc.appendChild) { cto_dis_doc.appendChild(cto_dis_im);}}}
}
document.write('<div id="pcto_dis_div" style="display:none"></div>')
document.write('<div style="display:none"><img src="http://bestbuyuk.widget.criteo.com/pac/display.js?p1='+escape('v=2&wi=7712143&pt1=2&i=Your item
id')+'&t1=sendEvent&resptype=gif&cb='+Math.floor(Math.random()*99999999999)+'" onload="pcto_dis();"/></div>');
</script>


Sale confirmation page:


<script type="text/javascript">
document.write('<div style="display:none"><img src="https://sslwidget.criteo.com/pac/display.js?p1='+escape('v=2&wi=7712144&t=Your transaction id&s=1&i1=First item id&p1=Single price of first item&q1=Quantity&i2=Second item id&p2=Single price of second item&q2=Quantity...')+'&t1=transaction&resptype=gif&cb='+Math.floor(Math.random()*99999999999)+'"/></div>');
</script>
```



You can get the necessary properties for MasterTag from the code above:


``` javascript

 AWIN.Tracking.Criteo.partnerId = 2305; // from parameter 'p' in the product tag

 AWIN.Tracking.Criteo.widgetId = "7712143";  // from parameter 'wi' in the product tag

 AWIN.Tracking.Criteo.saleWidgetId = "7712144"; // from parameter 'wi' in the sale tag

 AWIN.Tracking.Criteo.poolId = "pac"; // first path after "http://bestbuyuk.widget.criteo.com" in product tag

 AWIN.Tracking.Criteo.httpWidgetUrl = "http://bestbuyuk.widget.criteo.com"; //  cto_dis_im.src value in product tag
```



If you ever need to perform this sort of code work please consult team
Prime before you make it live.