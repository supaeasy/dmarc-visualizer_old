FROM grafana/grafana:10.1.5

USER root

ADD --chown=grafana:root Grafana-DMARC_Reports.json /var/lib/grafana/dashboards/

COPY grafana-provisioning/ /etc/grafana/provisioning/
RUN chmod 644 /etc/grafana/provisioning
RUN chown -R grafana:root /etc/grafana/provisioning/

##################################################################
## Customization depends on the Grafana version
## May work or not work for the version different from the current
## Check GitHub file history for the previous Grafana versions
##################################################################


##################################################################
## VISUAL
##################################################################

## Replace Favicon and Apple Touch
COPY images/favicon-32x32.png /usr/share/grafana/public/img/fav32.png
COPY images/apple-touch-icon.png /usr/share/grafana/public/img/apple-touch-icon.png

## Replace Logo
COPY images/logo.svg /usr/share/grafana/public/img/grafana_icon.svg

## Update Background
COPY images/background.svg /usr/share/grafana/public/img/g8_login_dark.svg
COPY images/background.svg /usr/share/grafana/public/img/g8_login_light.svg

##################################################################
## HANDS-ON
##################################################################

# Update Title
RUN sed -i 's|<title>\[\[.AppTitle\]\]</title>|<title>DMARC-Visualizer</title>|g' /usr/share/grafana/public/views/index.html

## Update Title
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|AppTitle="Grafana"|AppTitle="DMARC-Visualizer"|g' {} \;

## Update Login Title
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|LoginTitle="Welcome to Grafana"|LoginTitle="Welcome to DMARC-Visualizer"|g' {} \;

## Remove Documentation, Support, Community in the Footer
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|\[{target:"_blank",id:"documentation".*grafana_footer"}\]|\[\]|g' {} \;

## Remove Edition in the Footer
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|({target:"_blank",id:"license",.*licenseUrl})|()|g' {} \;

## Remove Version in the Footer
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|({target:"_blank",id:"version",.*CHANGELOG.md":void 0})|()|g' {} \;

## Remove New Version is available in the Footer
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|({target:"_blank",id:"updateVersion",.*grafana_footer"})|()|g' {} \;

## Remove News icon
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|..createElement(....,{className:.,onClick:.,iconOnly:!0,icon:"rss","aria-label":"News"})|null|g' {} \;

## Remove Open Source icon
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|.push({target:"_blank",id:"version",text:`${..edition}${.}`,url:..licenseUrl,icon:"external-link-alt"})||g' {} \;

##################################################################
## CLEANING Remove Native Data Sources
##################################################################

## Time series databases / Graphite
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/graphite
RUN rm -rf /usr/share/grafana/public/build/graphite*

## Time series databases / OpenTSDB
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/opentsdb
RUN rm -rf /usr/share/grafana/public/build/opentsdb*

## Time series databases / InfluxDB
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/influxdb
RUN rm -rf /usr/share/grafana/public/build/influxdb*

## SQL / Microsoft SQL Server
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/mssql
RUN rm -rf /usr/share/grafana/public/build/mssql*

## SQL / MySQL
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/mysql
RUN rm -rf /usr/share/grafana/public/build/mysql*

## Distributed tracing / Tempo
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/tempo
RUN rm -rf /usr/share/grafana/public/build/tempo*

## Distributed tracing / Jaeger
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/jaeger
RUN rm -rf /usr/share/grafana/public/build/jaeger*

## Distributed tracing / Zipkin
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/zipkin
RUN rm -rf /usr/share/grafana/public/build/zipkin*

## Cloud / Azure Monitor
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/azuremonitor
RUN rm -rf /usr/share/grafana/public/build/azureMonitor*

## Cloud / CloudWatch
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/cloudwatch
RUN rm -rf /usr/share/grafana/public/build/cloudwatch*

## Cloud / Google Cloud Monitoring
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/cloud-monitoring
RUN rm -rf /usr/share/grafana/public/build/cloudMonitoring*

## Profiling / Parca
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/parca
RUN rm -rf /usr/share/grafana/public/build/parca*

## Profiling / Phlare
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/phlare
RUN rm -rf /usr/share/grafana/public/build/phlare*

## Profiling / Pyroscope
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/grafana-pyroscope-datasource
RUN rm -rf /usr/share/grafana/public/build/pyroscope*

## Others / Alertmanager
RUN rm -rf /usr/share/grafana/public/app/plugins/datasource/alertmanager
RUN rm -rf /usr/share/grafana/public/build/alertmanager*

## Remove Cloud and Enterprise categories
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|.id==="enterprise"|.id==="notanenterprise"|g' {} \;
RUN find /usr/share/grafana/public/build/ -name *.js -exec sed -i 's|.id==="cloud"|.id==="notacloud"|g' {} \;

##################################################################
## CLEANING Remove Native Panels
##################################################################

## Alert list
RUN rm -rf /usr/share/grafana/public/app/plugins/panel/alertlist

## Annotations list
RUN rm -rf /usr/share/grafana/public/app/plugins/panel/annolist

## Dashboard list
RUN rm -rf /usr/share/grafana/public/app/plugins/panel/dashlist

## News
RUN rm -rf /usr/share/grafana/public/app/plugins/panel/news

## Table (old)
RUN rm -rf /usr/share/grafana/public/app/plugins/panel/table-old

## Traces
RUN rm -rf /usr/share/grafana/public/app/plugins/panel/traces

## Flamegraph
RUN rm -rf /usr/share/grafana/public/app/plugins/panel/flamegraph

##################################################################

EXPOSE 3000