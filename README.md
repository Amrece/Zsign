# Zsign
AMRECE


#!/bin/sh
BASEDIR=$(dirname "$0")

pathGroups="AMR"

numbersN="3"

for index in $numbersN
do
rm -rf "$BASEDIR"/"$pathGroups$index"/*.ipa 2>/dev/null
done

for index in $numbersN
do
cp -R "$BASEDIR"/"Home_in"/*.ipa "$BASEDIR"/$pathGroups$index/

for filenames in $(find "$BASEDIR"/$pathGroups$index -name "*.ipa" | sort -n); do
echo ------------ Start sign $filenames ------------
"$BASEDIR"/$pathGroups$index/zsign -k "$BASEDIR"/$pathGroups$index/Certificates.p12 -m "$BASEDIR"/$pathGroups$index/embedded.mobileprovision -z 9 -o $filenames $filenames
echo ------------ Finish sign $filenames ------------
done
done



