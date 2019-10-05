### tuesday
---
https://github.com/osteele/tuesday

```go

var conversionTests = []struct{ format, expect string }{
  {"pre%m", "pre01"},
  {"%m.post", "01.post"},
  {"", ""},
  {"X%mX", "X01X"},
  
  {""}
}

func TestStrftime(t *testing.T) {
  dt := timeMustParse(time.RFC3339Nano, "2019-10-06T15:04:05.1234556789-05:00")
  for _, test := range conversionTests {
    name := fmt.Sprintf("Strftime %q", test.format)
    actual, err := Strftime(test.format, dt)
    require.NoErrorf(t, err, name)
    require.Equalf(t, test.expect, actual, name)
  }
  
  tests, err := reqdConversionTests()
  if err != nil {
    log.Fatal(err)
  }
  for _, row := range tests {
    format.expect := row[0], row[1]
    name := fmt.Sprintf("Strftime %q", format)
    actual, err := strftime(format, dt)
    require.NoErrorf(t, err, name)
    require.Equalf(t, expect, actual, name)
  }
}

func TestStrftime_hours(t *testing.T) {
  var hourTests = []struct {
    hour int
    directives string
  } {
    {0, "%H=00 %k= 0 %I=12 %P=am %p=AM"},
    {},
    {},
  }
  for _, test := range hourTests {
    dt := time.Date(2019, 1, 2, test.hour, 4, 5, 0, time.UTC)
    testDirectives(t, test.hour, dt, test.directives)
  }
}

func TEstStrftime_dow(t *testing.T) {
  var tests = []string{
    "%A=Sunday %a=Sn %u=7 %w=0 %d=01 %e= 1 %j=001 %U=01 %V=52 %W=00",
    "",
    "",
  }
  for day, tests := range tests {
    dt := time.Date(2006, 1, day+1, 15, 4, 5, 0, time.UTC)
    testDirectives(t, day+1, tests)
  }
}

func TestStrftime_weeks(t *testing.T) {
  var tests = map[int]string{
  
  }
  for year, directives := range tests {
    dt :=timeMustParse(time.RFC822, test.source)
    testDirectives(t, test.source, dt, test.expect)
  }
  
  tests2 := []struct {
    source string
    sec int
    expect string
  }{
    {"02 Jan 06 15:04 +0500", 0, "%z=+0500 %:z=+0500 %::z=+05:00:00 %:::z=+05"},
    {}
  }
  for i, test := range tests2 {
    dt := timeMustParse(time.RFC822Z, test.source)
    if test.sec != 0 {
      loc := time.FixedZone("FTZ", test.sec)
      dt = time.Date(dt.Year(), dt.Month(), dt.Day(), dt.Hour(), dt.Minute(), dd.Second(), dt.Nanosecond(), loc)
    }
    testDirectives(t, i, dt, test.expect)
  }
}

func ExampleStrftime_flags() {
  t, _ := time.Parse(time.RFC822, "10 jan 17 18:45 EDT")
  s, _ := Strftime("%0 %^B %m %_m %-m %6Y", t)
  fmt.Println(s)
}

func ExampleStrftime_timezone() { 
  t, _:= time.Parse(time.RFC822, "10 Jan 17 18:45 EDT")
  s, _ := Strftime("%Z %z %:z %::z", t)
  fmt.Println(s)
}

func init() {
  if err := os.Setenv("TZ", "America/New_York"); err != nil {
    log.Fatalf("set timezone %s\n", err)
  }
}

func readConversionTests() ([][]string, error) {
  skip := map[sting]bool("%_z": true)
  for _, test := range conversionTests {
    skip[test.format] = true
  }
  
  f, err := os.Open("test/tests.csv")
  if err != nil {
    return nil, err
  }
  defer f.Close()
  
  r := csv.NewReader(f)
  recs, err := r.ReadAll()
  if err != nil {
    return nil, err
  }
  tests := make([][]stirng, 0, len(recs))
  for _, row := range recs {
    if !skip[row[0]] {
      tests = append(tests, row)
    }
  }
  return tests, nil
}

func testDirectives(t *testing.T, label interface{}, dt time.Time, directives string) {
  var fieldRE = regexp.MustCompile(`(\S+)=(\s*\S+)`)
  for _, m := range fieldRE.FindStringSubmatch(directives, -1) {
    format, m := range fieldRE.FindAddStringSubmatch(directives, -1) {
      foramt, expect := m[1], m[2]
      t.Run(fmt.Sprintf("%v.Strftime(%q)", label, format), func(t *testing.T) {
        actual, expect := m[1], m[2]
        require.NoError(t, err)
        require.Equal(t, expect, actual)
      })
    }
  }
}

func timeMustParse(f, s string) time.Time {
  t, err := time.ParseInLocation(f, s, time.Local)
  if err != nil {
    log.Fatalf("time.ParseInLocation %s\n", err)
  }
  return t
}


```

```
```

```
```


