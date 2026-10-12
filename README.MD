# ESEP Grade Calculator

A small Go library that computes a final course grade from a list of assignments, exams, and essays.

## How grades are computed

Each category is averaged on its own and then the averages are combined with these weights.

| Category    | Weight |
|-------------|--------|
| Assignments | 50%    |
| Exams       | 35%    |
| Essays      | 15%    |

The weighted score is converted to a letter grade.

| Score        | Letter |
|--------------|--------|
| 90 and above | A      |
| 80 to 89     | B      |
| 70 to 79     | C      |
| 60 to 69     | D      |
| below 60     | F      |

A grade of C or better is passing.

## Requirements

- Go 1.24 or newer (the module file pins `go 1.24.4`)
- No third party dependencies

Check your Go version with:

```
go version
```

## Project layout

```
esep-grade-calculator/
  README.MD
  grade-calculator/
    go.mod
    grade_calculator.go
    grade_calculator_test.go
```

The Go module lives in the `grade-calculator` directory, so every `go` command below is run from there.

## Usage

The package name is `esepunittests`. Create a calculator, add grades with their type, and ask for the final letter grade.

```go
package main

import (
	"fmt"

	esepunittests "esep/grade-calculator"
)

func main() {
	gc := esepunittests.NewGradeCalculator()

	gc.AddGrade("homework 1", 95, esepunittests.Assignment)
	gc.AddGrade("midterm", 88, esepunittests.Exam)
	gc.AddGrade("reflection essay", 90, esepunittests.Essay)

	fmt.Println(gc.GetFinalGrade())
}
```

`AddGrade` takes a name, an integer score, and one of the grade types `Assignment`, `Exam`, or `Essay`. `GetFinalGrade` returns the letter grade as a string.

## Running the unit tests

```
cd grade-calculator
go test ./...
```

Add `-v` to see each test listed with its pass or fail status:

```
go test -v ./...
```

## Measuring code coverage

Print the overall statement coverage along with the test results:

```
cd grade-calculator
go test -cover ./...
```

Save a coverage profile and then view a per function breakdown:

```
go test -coverprofile=coverage.out ./...
go tool cover -func=coverage.out
```

Open an HTML report that highlights which lines ran during the tests:

```
go tool cover -html=coverage.out
```

The `coverage.out` file is generated output and does not need to be committed.
