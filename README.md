<?xml version="1.0" encoding="UTF-8"?>
<Module>
<ModulePrefs title="menu portal BBVA1" >
        <Require feature="dynamic-height"/>   
        <Require feature="setprefs" />  
</ModulePrefs>  
<!--<UserPref name="VarrootSite" display_name="Root del Site" required="true" default_value="home"/>-->
<!--
<Content type="html" view="configuration" preferred_height="80">
<![CDATA[
        <style>
                input#VarrootSite {
           width: 300px;
          }               
        </style>
  
        <table width="100%" border="0" id="tablaconfig">           
                <tr>       
                        <td>
                                Root del Site: <input type="text" id="VarrootSite" value="__UP_VarrootSite__"   onchange="registra('VarrootSite')"/>                   
                        </td>
                </tr>
        </table>        
  
        <script type="text/javascript">           
                // Get userprefs
                var prefs = new gadgets.Prefs();           
                function registra(variable)
                {       
                        prefs.set(variable,document.getElementById(variable).value);
                }  
                gadgets.window.adjustHeight();
        </script>   
]]>
</Content>
-->
<Content type="html"><![CDATA[

<style type="text/css">
        /*
        This copyright notice must be kept untouched in the stylesheet at all times.
        The original version of this stylesheet and the associated (x)html
        is available at http://www.stunicholls.com/menu/jquery-dropline-7.html
        Copyright (c) 2005-2008 Stu Nicholls. All rights reserved.
        This stylesheet and the associated (x)html may be modified in any 
        way to fit your requirements.
        */

        #menu {
                margin-top:0px; 
                position:relative; 
                height:38px;
        }
        #dropline {
                position:relative; 
                font-size:12px; 
                height:38px; 
                background:url(https://bbvagcs.googlecode.com/svn/trunk/img/fondomenuhome38.png) no-repeat;
        }
        #dropline, 
        #dropline ul {
                padding:0px; 
                margin:0; 
                list-style:none; 
                width:948px;
        }
        #dropline table {
                border-collapse:collapse; 
                margin:-1px -10px 0 0; 
                padding:0; 
                width:0; 
                height:0; 
                font-size:12px;
        }
        #dropline li {
                float:left; 
                height:38px;
        }
        #dropline li a {
                float:left; 
                display:block; 
                height:37px; 
                line-height:38px; 
                padding:0 20px 0 10px; 
                font-family:arial, sans-serif; 
                font-size:11px; 
                color:#fff; 
                text-decoration:none; 
                font-weight:bold;
                padding:0px 19px 0px 10px;
        }
        #dropline li ul li a {
                color: rgb(102, 102, 102);
        }
        #dropline li a.principal { 
                color:#fff;
        }
        #dropline li a.down { 
                color:#fff; 
                background:url(https://bbvagcs.googlecode.com/svn/trunk/img/down.gif) no-repeat right center;
        }
        #dropline li ul li a.down {
                font-size:14px; 
                font-weight:bold;
        }
        #dropline li ul {
                position:absolute; 
                top:38px; 
                left:-9999px; 
                z-index:10; 
                background:url(https://bbvagcs.googlecode.com/svn/trunk/img/fade.png);
        }
        #dropline li ul.floatRight li {
                float:right;
        }

        #title-crumbs {
                        font-size:12px;
                        color:#3F78B2;
                        text-transform: capitalize;
                        margin-top: 7px;
                }
        a.linkBreadCrumb,
        a:visited.linkBreadCrumb {
                fon-weight: normal;
                font-size:12px;
                color:#3F78B2;
                text-decoration:none;
                text-transform: capitalize;
        }
        a:hover.linkBreadCrumb,
        a:active.linkBreadCrumb {
                font-style: normal;
                font-size:12px;
                color:#009EE5;
                fon-weight: normal;
                text-decoration:none;           
                text-transform: capitalize;
        } 
        .currentBreadCrumb {
                fon-weight: bold;
                font-size:12px;
                color:#009EE5;
                text-decoration:none;
                text-transform: capitalize;             
        }               
</style>

<script src="https://bbvagcs.googlecode.com/svn/trunk/js/jquery-1.js" type="text/javascript"></script>

<script type="text/javascript">

        $(document).ready(function()
        {
                $("#dropline li.current").children("ul").css("left", "0px").show();
                $("#dropline li.current").children(":first-child").css("color", "#c00");
                $("#dropline li").hover(function()
                {
                        if(this.className.indexOf("current") == -1)  
                        {
                                getCurrent = $(this).parent().children("li.current:eq(0)");
                                if(this.className.indexOf("top") != -1)  
                                {
                                        $(this).children("a:eq(0)").css("background-color","#2586d7");
                                }
                                else 
                                {
                                        $(this).children("a:eq(0)").css("color","#000");
                                }

                                if (getCurrent = 1) 
                                {
                                        $(this).parent().children("li.current:eq(0)").children("ul").hide();
                                }

                                $(this).children("ul:eq(0)").css("left", "0px").show();
                        }
                },function()
                        {
                                if(this.className.indexOf("current") == -1)  
                                {
                                        getCurrent = $(this).parent().children("li.current:eq(0)");

                                        if(this.className.indexOf("top") != -1) 
                                        {
                                                $(this).children("a:eq(0)").css("color","#fff");
                                                $(this).children("a:eq(0)").css("background-color","transparent");
                                        }
                                        else 
                                        {                                       
                                                $(this).children("a:eq(0)").css("color","#666");
                                        }

                                        if (getCurrent = 1 ) 
                                        {                                   
                                                $(this).parent().children("li.current:eq(0)").children("ul").show();
                                        }
                                        
                                        $(this).children("ul:eq(0)").css("left", "-99999px").hide();
                                }
                        }
                );
        });

        var prefs = new gadgets.Prefs();
        gadgets.util.registerOnLoadHandler(showBreadcrumbs);
        
        //console.debug('breadcrumbs.xml version 6');
        
        function indice (parametros, rootSite)
        {       
                for(var i=0; i<parametros.length; i++)
                {
                        if(parametros[i]== rootSite)
                        {
                                return i;
                        } 
                }       
        }
        
        function showBreadcrumbs()
        {
                // Construct the breadcrumb string
                //var rootSite = prefs.getString("VarrootSite");
                var rootSite = "global-product";
                var s ="";
                var i,j,k = 0;
                var base = "";
                var barra = "/";
                var parametros = gadgets.util.getUrlParameters()["parent"].split("/");  
                var indexroot = indice(parametros, rootSite);   
                
                for (i=0;i<parametros.length;i++)
                {                               
                        if(i<indexroot)
                        {
                                base = base + parametros[i]+ "/";                               
                        }
                        if (parametros[i] == rootSite) 
                        {       
                                s = "&nbsp;<a class=\'linkBreadCrumb\' href=\'"+ base + rootSite + barra + "\' target=\'_parent\' title=\' " + parametros[i].replace(/-/g," ") + "  \'>home</a>";
                        
                                for(j=i+1;j<parametros.length;++j)
                                {   
                                        var aux = parametros[j].replace(/-/g," ");                                              
                                        
                                        if (aux.indexOf("?")>1)
                                        {
                                                var auxMov = aux.split("?");
                                                var litEnlace = auxMov[0];
                                        }
                                        else
                                        {                                                       
                                                if (aux.indexOf("ficha")>-1)
                                                {                                                               
                                                        var litEnlace = "Ficha";
                                                }
                                                else if (aux.indexOf("detalle proyecto")>-1)
                                                {                                                               
                                                        var litEnlace = "Detalle Proyecto";
                                                }
                                                else if (aux.indexOf("contactos")>-1)
                                                {
                                                        var litEnlace = "Contactos";
                                                }
                                                else
                                                {                                                               
                                                        var litEnlace = aux;
                                                }
                                        }
                                        if (j<parametros.length-1)
                                        {
                                                s = s + "<a class=\'linkBreadCrumb\' href=\'"+ base  + rootSite + barra  + parametros[j] + barra + "\' target=\'_parent\' title=\'" + litEnlace + "\'> >&nbsp;" + litEnlace + "</a>";
                                                rootSite = rootSite + "/" + parametros[j];
                                        }
                                        else
                                        {                                               
                                                s = s + " ><span class=\'currentBreadCrumb\' + parametros[j] + barra + \' >&nbsp;" + litEnlace + "</span>";
                                        }
                                }
                        }
                }
                document.getElementById("title-crumbs").innerHTML = s;     
        }
</script>

<div id="content">
        
        <div id="menu">
                <ul id="dropline">
                        <li class="home"><a style="color:#fff;width:10px;margin-left:5px;" href="https://sites.google.com/a/bbva.com/sibos2014" target="_parent" onclick="mark"></a></li>
                        <li class="top"><a id="sibos2014" class="principal" href="https://sites.google.com/a/bbva.com/sibos2014/sibos2014" target="_parent">Sibos 2014</a>
                          <ul style="left:-99999px; display: none;" class="sub">
                                        
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/sibos2014/stand-bbva" target="_parent">Stand BBVA</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/sibos2014/attendance" target="_parent">Key Contacts / Attendance</a></li>
                                           <li><a href="https://drive.google.com/a/bbva.com/file/d/0B4tQb4HqBuEedEVVOEhPQW9pVmM/edit?usp=sharing" target="_parent">Overwiev Plan</a></li>
                                         <li><a href="http://www.sibos.com/exhibition/about-exhibition/exhibitor-list" target="_parent">Exhibitor list</a></li>
                                         <li><a href="https://sites.google.com/a/bbva.com/sibos2014/sibos2014/participants" target="_parent">Participants</a></li>
                                         <li><a href="https://sites.google.com/a/bbva.com/sibos2014/sibos2014/press" target="_parent">Press</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/sibos2014/transport" target="_parent">Transportation</a></li>
                                         </ul>
                        </li>
                        
                         <li class="top"><a id="accomodation" class="principal" href="https://sites.google.com/a/bbva.com/sibos2014/accomodation" target="_parent">Accommodation</a>
                        
                        </li>
                     
                        <li class="top"><a id="forums" class="principal" href="https://sites.google.com/a/bbva.com/sibos2014/forums" target="_parent">Forums</a>
                        <ul style="left:-99999px; display: none;" class="sub">
                                        
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/compliance-forum" target="_parent">Compliance</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/corporate-forum" target="_parent">Corporate</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/innotribe" target="_parent">Innotribe</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/investment-manager-forum" target="_parent">Investment Manager</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/market-infrastructures-forum" target="_parent">Market Infrastructures</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/sibos-university" target="_parent">Sibos University</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/standards-forum" target="_parent">Standards</a></li>
                                        <li><a href="https://sites.google.com/a/bbva.com/sibos2014/forums/technology-forum" target="_parent">Technology</a></li>
                                  
                                        
                                        
                                        
                        </ul>
                        </li>
                        <li class="top"><a id="agenda" class="principal" href="https://sites.google.com/a/bbva.com/sibos2014/meeting-agenda" target="_parent">Meeting agenda</a>
                        
                        </li>
                         <li class="top"><a id="other" class="principal" href="https://sites.google.com/a/bbva.com/sibos2014/other-information" target="_parent">Other Information</a>
                        <ul style="left:-99999px; display: none;" class="sub">
                                  <li><a href="https://sites.google.com/a/bbva.com/sibos2014/other-information" target="_parent" target="_parent">Free Wi-Fi</a></li>
                                        
                                        <li><a href="http://www.sibos.com/sites/default/files/Sibos_Boston_2014_Practical_Pocket_Guide.pdf" target="_parent">Practical Pocket Guide</a></li>
                                        </ul>
                       
                        
                        </li>
                        
                </ul>
        </div>

        <!-- breadcrumbs-->
        <div id="title-crumbs">breadcrumbs</div>

        <!-- Elemento de menú set visited -->
        <script type="text/javascript">
        gadgets.util.registerOnLoadHandler(datospagina);
        function datospagina()
        {
                var parametros = gadgets.util.getUrlParameters()["parent"];     
                if (parametros.indexOf("sibos2014")!=-1)
                {
                        document.getElementById("sibos2014").style.backgroundColor = "#2586D7";
                }
                if (parametros.indexOf("forums")!=-1)
                {
                        document.getElementById("forums").style.backgroundColor = "#2586d7";
                }
                if (parametros.indexOf("agenda")!=-1)
                {
                        document.getElementById("agenda").style.backgroundColor = "#2586d7";
                }
                 if (parametros.indexOf("accomodation")!=-1)
                {
                        document.getElementById("agenda").style.backgroundColor = "#2586d7";
                }
                 if (parametros.indexOf("other")!=-1)
                {
                        document.getElementById("agenda").style.backgroundColor = "#2586d7";
                }
                
                        
        }
        </script>

<!--Fin of the Breadcrumbs-->
</div> 
<!-- end of content -->
]]></Content>
</Module>
