# Google Sheets

## Snippets

### Data Lookups

```
=INDEX(array, row_num, [column_num])
```

```
=MATCH(lookup_value, lookup_array, [match_type])
```

```
=index(DATA!$A2:$A, match($A2, DATA!$B2:$B, 0), 0)
```


```
=VLOOKUP(lookup_value, table_array, col_index_number, [range_lookup])
```


### SNAME
```
=LOWER(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE($C2, "-", ""), "’", ""), "'", ""), ".", ""), " ", ""), "ñ", "n"), "á", "a"), "í", "i"), ",","") )
```