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
