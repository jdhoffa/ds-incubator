# 2020-02-18: Testing

From <https://r-pkgs.org/tests.html>



## Why testing?

* Discuss



## Set up

```R
usethis::use_testthat()
```

Among other things, `usethis::use_testthat()` attaches testthat in tests/testthat.R


```r
library(testthat)
```



## Workflow

* Modify your code or tests.
* Test your package with Ctrl/Cmd + Shift + T or devtools::test().
* Repeat until all tests pass.



## Tests structure

If R/max_minus_min.R contains:


```r
max_minus_min <- function(x) {
  max(x) - min(x)
}
```

Then tests/testthat/test-max_minus_min.R may contains:


```r
test_that("max_minus_min with simple good input returns expected output", {
  expect_equal(max_minus_min(2:1), 1)
  expect_equal(max_minus_min(2:1), 1)
})
```



## What to test

> Whenever you are tempted to type something into a print statement or a debugger expression, write it as a test instead. -- Martin Fowler

> A QA engineer walks into a bar. Oders a beer. Orders 0 beers. Orders 9999999 beers. Orders a lizard. Orders -1 beers. Orders a afdelijknesv. -- Bill Sempf (@sempf) on Twitter


* Test what should work.


```r
test_that("max_minus_min with simple good input returns expected output", {
  expect_equal(max_minus_min(2:1), 1)
  expect_equal(max_minus_min(2:1), 1)
})
```

* Test what should fail.


```r
test_that("max_minus_min with bad input throws an error", {
  expect_error(max_minus_min(letters), "non-numeric argument")
})
```

* Edge cases.


```r
test_that("max_minus_min with edge cases behaves as expected", {
  expect_equal(max_minus_min(NA_integer_), NA_integer_)
  
  # Oh no! I need to modify my code until this test passes
  expect_equal(max_minus_min(c(1, 2, NA)), 1)
})
#> Error: Test failed: 'max_minus_min with edge cases behaves as expected'
#> * <text>:5: max_minus_min(c(1, 2, NA)) not equal to 1.
#> 1/1 mismatches
#> [1] NA - 1 == NA
```



## Questions

1. Do I need a package to test?
2. What are common expectations?
3. How can I test that the data my code needs hasn't change?
4. How can I test messages, warnings, errors?
5. How often should I test?