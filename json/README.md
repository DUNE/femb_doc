JSON files are used for at least two things in the femb tests:

* input `params.json` file
* summary output file

Some tests produce various other JSON files.

## Getting JSON files

A cronjob syncs JSON files from the `hothdaq`s to `hothstor2`.  This is available on the local file system at:

```
/dsk/1/data/sync-json/hothdaq[1-5]/dsk/[12]/oper/
```

And on the internatl BNL wired network or private lab network under:

http://hothstor2.phy.bnl.gov/~arch/sync-json/

## Playing with JSON

Due to JSON's structure, the usual unix command line tools do not work so well.  The `jq` command brings a lot of power.

* https://stedolan.github.io/jq/manual/

Trivial example usage:

```
bviren@hothstor2:~$ jq 'keys' /dsk/1/data/sync-json/hothdaq5/dsk/1/oper/adcasic/adcTest_P1single_hothdaq5_cold/20170713T171609/adcTest_20170713T171609_8.json
[
  "board_id",
  "dc",
  "dynamic",
  "error",
  "hostname",
  "inputPin",
  "operator",
  "serial",
  "static",
  "sumatra",
  "testResults",
  "timestamp"
]

bviren@hothstor2:~$ jq '.testResults.pass' /dsk/1/data/sync-json/hothdaq5/dsk/1/oper/adcasic/adcTest_P1single_hothdaq5_cold/20170713T171609/adcTest_20170713T171609_8.json
false
bviren@hothstor2:~$ for n in /dsk/1/data/sync-json/hothdaq5/dsk/1/oper/adcasic/*/*/adcTest_*.json
do
  echo $(jq '[.board_id, .serial, .testResults.pass]' $n)
done
[ "8", 110, true ]
[ "8", 138, true ]
[ "8", 139, true ]
...
```

Generate a JSON file with a summary of many summaries:

```
jq -s '[.[] | {"timestamp":.timestamp, "board_id":.board_id, "serial":.serial, "pass":.testResults.pass, "datadir":.sumatra.datadir}]' \
   /dsk/1/data/sync-json/hothdaq5/dsk/1/oper/adcasic/*/*/adcTest_*.json \
   > public_html/adc-summary.json
```

Maybe JSON isn't the best format for some report or further processing.  It is easy to massage JSON into other forms using templates.

```
$ virtualenv venv
$ source venv/bin/activate
$ pip install j2cli
$ j2 adc-summary.txt.j2 adc-summary.json > adc-summary.txt
```

Where `j2` is from the [j2cli](https://github.com/kolypto/j2cli) package and is used to apply 
the JSON to a [Jinja2](http://jinja.pocoo.org/docs/2.9/templates/) template and spit out something new.
In this example the template just turns each summary dictionary into a line:

```
{% for item in summary %}{{item.timestamp}} {{item.board_id}} {{item.serial}} {{item.pass}} {{item.datadir}}
{% endfor %}
```

The resultinf text file is then:

```
20170621T103851 8 110 True /dsk/1/data/oper/adcasic/adcTest_P1single_hothdaq4/20170621T103851
20170621T113213 8 138 True /dsk/1/data/oper/adcasic/adcTest_P1single_hothdaq4/20170621T113213
20170621T121549 8 139 True /dsk/1/data/oper/adcasic/adcTest_P1single_hothdaq4/20170621T121549
...
```

