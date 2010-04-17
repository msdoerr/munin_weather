#!/bin/sh
#
#       Munin plugin:
#               read data from WS2300 weather station
#               and let munin make pretty graphs
#
# msd, 17-apr-2010, v1.0:       get in/outside temperatures and humidities
#

WEATHER=/home/ws2300
CONFIG=$WEATHER/open2300.conf
FETCH=$WEATHER/fetch2300

###     "configuration" sections

RET=0
if [ "$#" -gt 0 ] ; then

    if [ "$1" = "autoconf" ] ; then

        if [ -f "$CONFIG" -a -x "$FETCH" ] ; then
            echo "yes"
        else
            echo "no (ws2300 not found)"
            RET=1
        fi

    elif [ "$1" = "config" ] ; then

        echo "graph_title WS2300"
        #echo "graph_args --base 1000 -l -20 -m 50"
        echo "graph_category Weather"
        echo "graph_info In/Outside temperature and humidity"
        echo "graph_vlabel 'Temp. in C / Humidity in %'"

        echo "Tin.label Tin"
        echo "Tout.label Tout"
        echo "Hin.label Hin"
        echo "Hout.label Hout"

    fi

    exit $RET
fi

###     "data" section

$FETCH $CONFIG | awk '
$1 == "Ti"      { print "Tin.value " $2 }
$1 == "To"      { print "Tout.value " $2 }
$1 == "RHi"     { print "Hin.value " $2 }
$1 == "RHo"     { print "Hout.value " $2 }
'

exit 0

