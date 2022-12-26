inputFile = LOAD 'hdfs:///ProjectActivity1/' USING PigStorage('\t') AS (name: chararray, line: chararray);

grpd = GROUP inputFile BY name;

names = FOREACH grpd GENERATE $0,COUNT($1) AS no_of_lines;

namesOrdered = ORDER names BY no_of_lines DESC;

STORE namesOrdered INTO 'hdfs:///user/sreedevi/ProjAct1/output';