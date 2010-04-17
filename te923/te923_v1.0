#!/bin/sh
#
#       Munin plugin:
#               read data from TE923 weather station
#               and let munin make pretty graphs
#
# msd, 17-apr-2010, v1.0:       get temperatures and humidities from
#                               base station and 5 additional sensors
#

WEATHER=/home/te923
FETCH=$WEATHER/te923con

###     "configuration" sections

RET=0
if [ "$#" -gt 0 ] ; then

    if [ "$1" = "autoconf" ] ; then

        if [ -x "$FETCH" ] ; then
            echo "yes"
        else
            echo "no (te923con not found)"
            RET=1
        fi

    elif [ "$1" = "config" ] ; then

        echo "graph_title TE923"
        #echo "graph_args --base 1000 -l -20 -m 50"
        echo "graph_category Weather"
        echo "graph_info Temperature and Humidity"
        echo "graph_vlabel 'Temp. in C / Humidity in %'"

        echo "T0.label T0"
        echo "T1.label T1"
        echo "T2.label T2"
        echo "T3.label T3"
        echo "T4.label T4"
        echo "T5.label T5"
        echo "H0.label H0"
        echo "H1.label H1"
        echo "H2.label H2"
        echo "H3.label H3"
        echo "H4.label H4"
        echo "H5.label H5"

    fi

    exit $RET
fi

###     "data" section

$FETCH | awk -F: '{
print "T0.value " $2 ;
print "T1.value " $4 ;
print "T2.value " $6 ;
print "T3.value " $8 ;
print "T4.value " $10 ;
print "T5.value " $12 ;
print "H0.value " $3 ;
print "H1.value " $5 ;
print "H2.value " $7 ;
print "H3.value " $9 ;
print "H4.value " $11 ;
print "H5.value " $13 ;
'

exit 0

