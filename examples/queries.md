## Ejemplos de consultas sobre presupuestos

A continuación se presentan algunos ejemplos de consultas utilizando como referencia un extracto de los  conjuntos de datos de presupuestos publicados por el ayuntamiento de Madrid como datos abiertos. Se han utilizado los grafos de http://vocab.ciudadesabiertas.es/datosabiertos/grafo-recurso/hacienda/presupuesto/datos-madrid. Además se tienen los siguientes grafos:
skos programa-gasto http://vocab.linkeddata.es/datosabiertos/grafo-skos/hacienda/presupuesto/programa-gasto
skos economica-ingreso http://vocab.linkeddata.es/datosabiertos/grafo-skos/hacienda/presupuesto/economica-ingreso
skos economica-gasto http://vocab.linkeddata.es/datosabiertos/grafo-skos/hacienda/presupuesto/economica-gastohttp://vocab.ciudadesabiertas.es/datosabiertos/grafo-recurso/hacienda/presupuesto/datos-madrid

Por ejemplo, en esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdatosabiertos%2Fgrafo-recurso%2Fhacienda%2Fpresupuesto%2Fdatos-madrid&query=PREFIX+espresup%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fhacienda%2Fpresupuesto%23%3E%0D%0APREFIX+time%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2006%2Ftime%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0A%0D%0ASELECT++%3Fgasto+%3FcreditoPresInicial++%3FlabelPrograma+%3FlabelEconomica+%3FlabelOrganica+%0D%0AWHERE+%7B+%3Fgasto+a+espresup%3APresupuestoGasto+.%0D%0A++++++++%3Fgasto+espresup%3AcreditoPresupuestarioInicial+%3FcreditoPresInicial+.%0D%0A++++++++%3Fgasto+espresup%3AclasificacionPrograma+%3Fprograma+.%0D%0A+++++++%3Fprograma+skos%3AprefLabel+%3FlabelPrograma+.%0D%0A+++++++%3Fgasto+espresup%3AclasificacionEconomicaGasto+%3Feconomica+.%0D%0A+++++++%3Feconomica+skos%3AprefLabel+%3FlabelEconomica+.%0D%0A+++++++OPTIONAL+%7B%3Fgasto+espresup%3AclasificacionOrganica+%3Forganica+.+%3Forganica+skos%3AprefLabel+%3FlabelOrganica%7D%0D%0A%7D%0D%0A%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se pregunta el presupuesto de gastos de Madrid para el 2018 (se da una muestra del presupuesto).  
```
PREFIX espresup:<http://vocab.ciudadesabiertas.es/def/hacienda/presupuesto#>
PREFIX time:<http://www.w3.org/2006/time#>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>


SELECT  ?gasto ?creditoPresInicial  ?labelPrograma ?labelEconomica ?labelOrganica 
WHERE { ?gasto a espresup:PresupuestoGasto .
        ?gasto espresup:creditoPresupuestarioInicial ?creditoPresInicial .
        ?gasto espresup:clasificacionPrograma ?programa .
       ?programa skos:prefLabel ?labelPrograma .
       ?gasto espresup:clasificacionEconomicaGasto ?economica .
       ?economica skos:prefLabel ?labelEconomica .
       OPTIONAL {?gasto espresup:clasificacionOrganica ?organica . ?organica skos:prefLabel ?labelOrganica}
}


```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdatosabiertos%2Fgrafo-recurso%2Fhacienda%2Fpresupuesto%2Fdatos-madrid&query=PREFIX+espresup%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fhacienda%2Fpresupuesto%23%3E%0D%0APREFIX+time%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2006%2Ftime%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+xsd%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0D%0A%0D%0ASELECT++%3FejecucionGasto+%3FcredInicial+%3FcredModificac+%3FcredDefinitivo+%3FcredAutorizado+%3FobligReconocidas++%0D%0AWHERE+%7B+%3FejecucionGasto+a+espresup%3AEjecucionGasto+.%0D%0A++++++++%3FejecucionGasto+espresup%3AperiodoEjecucion+%3FintervaloPropio+.%0D%0A++++++++%3FintervaloPropio+time%3AhasEnd+%3FintanciaTiempo+.%0D%0A++++++++%3FinstanciaTiempo+time%3AinXSDgYearMonth+%3FfechaEjecucion+.%0D%0A++++++++%3FejecucionGasto+espresup%3AgastoEjecutado+%3Fgasto+.%0D%0A++++++++%3Fgasto+espresup%3AcreditoPresupuestarioInicial+%3FcredInicial+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoModificaciones+%3FcredModificac+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoDefinitivoVigente+%3FcredDefinitivo+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoAutorizado+%3FcredAutorizado+.%0D%0A++++++++%3FejecucionGasto+espresup%3AobligacionesReconocidasNetas+%3FobligReconocidas++.%0D%0A++++++++FILTER%28%3FfechaEjecucion+%3D+%222018-12%22%5E%5Exsd%3AgYearMonth%29+%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se pregunta cuál es la ejecución del presupuesto de gastos para diciembre de 2018 (se da una muestra de la ejecución).
PREFIX espresup:<http://vocab.ciudadesabiertas.es/def/hacienda/presupuesto#>
PREFIX time:<http://www.w3.org/2006/time#>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>
PREFIX xsd:<http://www.w3.org/2001/XMLSchema#>

SELECT  ?ejecucionGasto ?credInicial ?credModificac ?credDefinitivo ?credAutorizado ?obligReconocidas  
WHERE { ?ejecucionGasto a espresup:EjecucionGasto .
        ?ejecucionGasto espresup:periodoEjecucion ?intervaloPropio .
        ?intervaloPropio time:hasEnd ?intanciaTiempo .
        ?instanciaTiempo time:inXSDgYearMonth ?fechaEjecucion .
        ?ejecucionGasto espresup:gastoEjecutado ?gasto .
        ?gasto espresup:creditoPresupuestarioInicial ?credInicial .
        ?ejecucionGasto espresup:creditoModificaciones ?credModificac .
        ?ejecucionGasto espresup:creditoDefinitivoVigente ?credDefinitivo .
        ?ejecucionGasto espresup:creditoAutorizado ?credAutorizado .
        ?ejecucionGasto espresup:obligacionesReconocidasNetas ?obligReconocidas  .
        FILTER(?fechaEjecucion = "2018-12"^^xsd:gYearMonth) 
}

En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdatosabiertos%2Fgrafo-recurso%2Fhacienda%2Fpresupuesto%2Fdatos-madrid&query=PREFIX+espresup%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fhacienda%2Fpresupuesto%23%3E%0D%0APREFIX+time%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2006%2Ftime%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+xsd%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0D%0APREFIX+skos-programa%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Fprograma-gasto%2Fmadrid%2F%3E%0D%0APREFIX+skos-economica%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Feconomica-gasto%2Fmadrid%2F%3E%0D%0A%0D%0ASELECT++%3FejecucionGasto+%3FcredInicial+%3FcredModificac+%3FcredDefinitivo+%3FcredAutorizado+%3FobligReconocidas+%0D%0AWHERE+%7B+%3FejecucionGasto+a++espresup%3AEjecucionGasto+.%0D%0A++++++++%3FejecucionGasto+espresup%3AperiodoEjecucion+%3FintervaloPropio+.%0D%0A++++++++%3FintervaloPropio+time%3AhasEnd+%3FintanciaTiempo+.%0D%0A++++++++%3FinstanciaTiempo+time%3AinXSDgYearMonth+%3FfechaEjecucion+.%0D%0A++++++++%3FejecucionGasto+espresup%3AgastoEjecutado+%3Fgasto+.%0D%0A++++++++%3Fgasto+espresup%3AcreditoPresupuestarioInicial+%3FcredInicial+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoModificaciones+%3FcredModificac+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoDefinitivoVigente+%3FcredDefinitivo+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoAutorizado+%3FcredAutorizado+.%0D%0A++++++++%3FejecucionGasto+espresup%3AobligacionesReconocidasNetas+%3FobligReconocidas++.%0D%0A++++++++%3Fgasto+espresup%3AclasificacionEconomicaGasto+skos-economica%3A22602+.%0D%0A++++++++%23%3Fgasto+espresup%3AclasificacionPrograma+skos-programa%3A23270+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoAutorizado+%3FcredAutorizado+.%0D%0A++++++++%3FejecucionGasto+espresup%3AobligacionesReconocidasNetas+%3FobligReconocidas++.%0D%0A++++++++FILTER%28%3FfechaEjecucion+%3D+%222018-12%22%5E%5Exsd%3AgYearMonth%29%0D%0A%7D+&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se pregunta cuál es el gasto ejecutado para una determinada clasificacion economica y de programa, en este caso el el Programa  23270 - PROMOCIÓN PLAN DERECHOS HUMANOS y la clasificación económica - 22602 - PUBLICIDAD Y PROPAGANDA.

PREFIX espresup:<http://vocab.ciudadesabiertas.es/def/hacienda/presupuesto#>
PREFIX time:<http://www.w3.org/2006/time#>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>
PREFIX xsd:<http://www.w3.org/2001/XMLSchema#>
PREFIX skos-programa:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/programa-gasto/madrid/>
PREFIX skos-economica:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/economica-gasto/madrid/>

SELECT  ?ejecucionGasto ?credInicial ?credModificac ?credDefinitivo ?credAutorizado ?obligReconocidas 
WHERE { ?ejecucionGasto a  espresup:EjecucionGasto .
        ?ejecucionGasto espresup:periodoEjecucion ?intervaloPropio .
        ?intervaloPropio time:hasEnd ?intanciaTiempo .
        ?instanciaTiempo time:inXSDgYearMonth ?fechaEjecucion .
        ?ejecucionGasto espresup:gastoEjecutado ?gasto .
        ?gasto espresup:creditoPresupuestarioInicial ?credInicial .
        ?ejecucionGasto espresup:creditoModificaciones ?credModificac .
        ?ejecucionGasto espresup:creditoDefinitivoVigente ?credDefinitivo .
        ?ejecucionGasto espresup:creditoAutorizado ?credAutorizado .
        ?ejecucionGasto espresup:obligacionesReconocidasNetas ?obligReconocidas  .
        ?gasto espresup:clasificacionEconomicaGasto skos-economica:22602 .
        #?gasto espresup:clasificacionPrograma skos-programa:23270 .
        ?ejecucionGasto espresup:creditoAutorizado ?credAutorizado .
        ?ejecucionGasto espresup:obligacionesReconocidasNetas ?obligReconocidas  .
        FILTER(?fechaEjecucion = "2018-12"^^xsd:gYearMonth)
} 

En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdatosabiertos%2Fgrafo-recurso%2Fhacienda%2Fpresupuesto%2Fdatos-madrid&query=PREFIX+espresup%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fhacienda%2Fpresupuesto%23%3E%0D%0APREFIX+skos-inversion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Finversion%2Fmadrid%2F%3E%0D%0APREFIX+skos-programa%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Fprogramas-gasto%2Fmadrid%2F%3E%0D%0APREFIX+dct%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A%0D%0ASELECT++%3FidInversion+%3Fdenominacion+%3FlabelLinea+%3FlabelSublinea+%3FlabelDistrito++%0D%0AWHERE+%7B+%0D%0A++++++++%3Finversion+a+espresup%3AInversionFinancieramenteSostenible+.%0D%0A++++++++%3Finversion+dct%3Aidentifier+%3FidInversion+.%0D%0A++++++++%3Finversion+dct%3Adescription+%3Fdenominacion+.%0D%0A++++++++%3Finversion+espresup%3AclasificacionInversion+%3Fsublinea+.%0D%0A++++++++%3Fsublinea+skos%3AprefLabel+%3FlabelSublinea+.%0D%0A++++++++%3Fsublinea+skos%3Abroader+%3Flinea+.%0D%0A++++++++%3Flinea+skos%3AprefLabel+%3FlabelLinea+.%0D%0A++++++++%3Finversion+espresup%3Aambito+%3Fdistrito+.%0D%0A++++++++%3Fdistrito+rdf%3Alabel+%3FlabelDistrito+.%0D%0A++++++++%3Finversion+espresup%3AambitoGlobalCiudad++%22false%22%5E%5Exsd%3Aboolean+.%0D%0A++++++++%7D&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se pregunta cuales son las inversiones financieramwente sostenibles de Madrid.

PREFIX espresup:<http://vocab.ciudadesabiertas.es/def/hacienda/presupuesto#>
PREFIX skos-inversion:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/inversion/madrid/>
PREFIX skos-programa:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/programas-gasto/madrid/>
PREFIX dct:<http://purl.org/dc/terms/>

SELECT  ?idInversion ?denominacion ?labelLinea ?labelSublinea ?labelDistrito  
WHERE { 
        ?inversion a espresup:InversionFinancieramenteSostenible .
        ?inversion dct:identifier ?idInversion .
        ?inversion dct:description ?denominacion .
        ?inversion espresup:clasificacionInversion ?sublinea .
        ?sublinea skos:prefLabel ?labelSublinea .
        ?sublinea skos:broader ?linea .
        ?linea skos:prefLabel ?labelLinea .
        ?inversion espresup:ambito ?distrito .
        ?distrito rdf:label ?labelDistrito .
        ?inversion espresup:ambitoGlobalCiudad  "false"^^xsd:boolean .
        }

En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdatosabiertos%2Fgrafo-recurso%2Fhacienda%2Fpresupuesto%2Fdatos-madrid&query=PREFIX+espresup%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fhacienda%2Fpresupuesto%23%3E%0D%0APREFIX+skos-inversion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Finversion%2Fmadrid%2F%3E%0D%0APREFIX+skos-programa%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Fprogramas-gasto%2Fmadrid%2F%3E%0D%0APREFIX+dct%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A%0D%0A%0D%0A%0D%0ASELECT++%3FidInversion+%3Fdenominacion+%3FlabelLinea+%3FlabelSublinea+%0D%0AWHERE+%7B+%0D%0A++++++++%3Finversion+a+espresup%3AInversionFinancieramenteSostenible+.%0D%0A++++++++%3Finversion+dct%3Aidentifier+%3FidInversion+.%0D%0A++++++++%3Finversion+dct%3Adescription+%3Fdenominacion+.%0D%0A++++++++%3Finversion+espresup%3AclasificacionInversion+%3Fsublinea+.%0D%0A++++++++%3Fsublinea+skos%3AprefLabel+%3FlabelSublinea+.%0D%0A++++++++%3Fsublinea+skos%3Abroader+%3Flinea+.%0D%0A++++++++%3Flinea+skos%3AprefLabel+%3FlabelLinea+.%0D%0A++++++++%3Finversion+espresup%3Aambito+%3Fdistrito+.%0D%0A++++++++%3Fdistrito+rdf%3Alabel+%3FlabelDistrito+.%0D%0A++++++++FILTER+%28CONTAINS%28%3FlabelDistrito%2C%22PUENTE+DE+VALLECAS%22%29%29%0D%0A++++++++%7D&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se pregunta cuales son las inversiones financieramente sostenibles de un cierto distrito, en este caso el distrito PUENTE DE VALLECAS.

PREFIX espresup:<http://vocab.ciudadesabiertas.es/def/hacienda/presupuesto#>
PREFIX skos-inversion:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/inversion/madrid/>
PREFIX skos-programa:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/programas-gasto/madrid/>
PREFIX dct:<http://purl.org/dc/terms/>

SELECT  ?idInversion ?denominacion ?labelLinea ?labelSublinea 
WHERE { 
        ?inversion a espresup:InversionFinancieramenteSostenible .
        ?inversion dct:identifier ?idInversion .
        ?inversion dct:description ?denominacion .
        ?inversion espresup:clasificacionInversion ?sublinea .
        ?sublinea skos:prefLabel ?labelSublinea .
        ?sublinea skos:broader ?linea .
        ?linea skos:prefLabel ?labelLinea .
        ?inversion espresup:ambito ?distrito .
        ?distrito rdf:label ?labelDistrito .
        FILTER (CONTAINS(?labelDistrito,"PUENTE DE VALLECAS"))
        }

En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=http%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdatosabiertos%2Fgrafo-recurso%2Fhacienda%2Fpresupuesto%2Fdatos-madrid&query=PREFIX+espresup%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fhacienda%2Fpresupuesto%23%3E%0D%0APREFIX+skos-inversion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Finversion%2Fmadrid%2F%3E%0D%0APREFIX+skos-programa%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Fprogramas-gasto%2Fmadrid%2F%3E%0D%0APREFIX+dct%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A%0D%0ASELECT++%3Fdenominacion+%3Fimporte+%3FpresInversion+%3FcredInicial+%3FcredModificac+%3FcredDefinitivo+%3FcredAutorizado+%3FobligReconocidas%0D%0AWHERE+%7B%0D%0A++++++++%3Finversion+a+espresup%3AInversionFinancieramenteSostenible+.%0D%0A++++++++%3Finversion+dct%3Aidentifier+%222018-000536%22+.%0D%0A++++++++%3Finversion+dct%3Adescription+%3Fdenominacion+.%0D%0A++++++++%3Finversion+espresup%3Aimporte+%3Fimporte+.%0D%0A++++++++%3Finversion+espresup%3ApresupuestoInversion+%3FpresInversion+.%0D%0A++++++++%3FpresInversion+espresup%3AcreditoPresupuestarioInicial+%3FcredInicial+.%0D%0A++++++++%3FejecucionGasto+espresup%3AgastoEjecutado+%3FpresInversion+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoModificaciones+%3FcredModificac+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoDefinitivoVigente+%3FcredDefinitivo+.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoAutorizado+%3FcredAutorizado+.%0D%0A++++++++%3FejecucionGasto+espresup%3AobligacionesReconocidasNetas+%3FobligReconocidas++.%0D%0A++++++++%3FejecucionGasto+espresup%3AcreditoAutorizado+%3FcredAutorizado+.%0D%0A++++++++%3FejecucionGasto+espresup%3AobligacionesReconocidasNetas+%3FobligReconocidas++.%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se pregunta cuales son los gastos presupuestados y la ejecución para una determinada inversión, en este caso la inversión con el identificador 2018-000536.

PREFIX espresup:<http://vocab.ciudadesabiertas.es/def/hacienda/presupuesto#>
PREFIX skos-inversion:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/inversion/madrid/>
PREFIX skos-programa:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/programas-gasto/madrid/>
PREFIX dct:<http://purl.org/dc/terms/>

SELECT  ?denominacion ?importe ?presInversion ?credInicial ?credModificac ?credDefinitivo ?credAutorizado ?obligReconocidas
WHERE {
        ?inversion a espresup:InversionFinancieramenteSostenible .
        ?inversion dct:identifier "2018-000536" .
        ?inversion dct:description ?denominacion .
        ?inversion espresup:importe ?importe .
        ?inversion espresup:presupuestoInversion ?presInversion .
        ?presInversion espresup:creditoPresupuestarioInicial ?credInicial .
        ?ejecucionGasto espresup:gastoEjecutado ?presInversion .
        ?ejecucionGasto espresup:creditoModificaciones ?credModificac .
        ?ejecucionGasto espresup:creditoDefinitivoVigente ?credDefinitivo .
        ?ejecucionGasto espresup:creditoAutorizado ?credAutorizado .
        ?ejecucionGasto espresup:obligacionesReconocidasNetas ?obligReconocidas  .
        ?ejecucionGasto espresup:creditoAutorizado ?credAutorizado .
        ?ejecucionGasto espresup:obligacionesReconocidasNetas ?obligReconocidas  .
}


