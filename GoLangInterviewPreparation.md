## Golang Preparation
 ## Varible declarations
	* var age int
    	  age = 25
	* age:=25 inside function only
	*  var x, y, z int = 1, 2, 3
   	   a, b := "Go", true
	* var (
    		language = "Go"
    		version  = 1.21
    		isFun    = true
	)
## primatives
	Integers
		Signed integers:
			int (size depends on machine: 32 or 64 bits)
			int8 (−128 to 127)
			int16 (−32,768 to 32,767)
			int32 (−2,147,483,648 to 2,147,483,647)
			int64 (−9,223,372,036,854,775,808 to 9,223,372,036,854,775,807)

		Unsigned integers:
			uint (size depends on machine: 32 or 64 bits)
			uint8 (0 to 255) → alias: byte
			uint16 (0 to 65,535)
			uint32 (0 to 4,294,967,295)
			uint64 (0 to 18,446,744,073
	float32 (approx 6–7 decimal digits)
	float64 (approx 15–16 decimal digits, default for decimals)

		Boolean	bool
		Integers	int, int8, int16, int32, int64, uint, uint8 (byte), uint16, uint32, uint64
		Float	float32, float64
		Complex	complex64, complex128
		Text	string, rune (int32), byte (uint8)
	**Array**
		var arr [5]int = [5]int{1, 2, 3, 4, 5}
		matrix := [3][4]int{
    				{1, 2, 3, 4},
				{5, 6, 7, 8},
				{9, 10, 11, 12},
				}
     **Slice**
	numbers := []int{1, 2, 3}
	numbers = append(numbers, 4, 5) //
package sliceutils
a[:index] return array before that index
a[index:] return array after that index
... stread array into individual items
// Insert inserts a value at the given index in a slice.
func Insert[T any](s []T, index int, value T) []T {
	if index < 0 || index > len(s) {
		panic("index out of range")
	}
	return append(s[:index], append([]T{value}, s[index:]...)...)
}

// Delete removes the element at the given index.
func Delete[T any](s []T, index int) []T {
	if index < 0 || index >= len(s) {
		panic("index out of range")
	}
	return append(s[:index], s[index+1:]...)
}

// Update replaces the element at the given index with a new value.
func Update[T any](s []T, index int, value T) []T {
	if index < 0 || index >= len(s) {
		panic("index out of range")
	}
	s[index] = value
	return s
}

// Pop removes and returns the last element.
func Pop[T any](s []T) ([]T, T) {
	if len(s) == 0 {
		panic("cannot pop from empty slice")
	}
	val := s[len(s)-1]
	return s[:len(s)-1], val
}

// Shift removes and returns the first element.
func Shift[T any](s []T) ([]T, T) {
	if len(s) == 0 {
		panic("cannot shift from empty slice")
	}
	val := s[0]
	return s[1:], val
}

// Unshift adds an element at the beginning.
func Unshift[T any](s []T, value T) []T {
	return append([]T{value}, s...)
}

// Extend concatenates two slices.
func Extend[T any](s, t []T) []T {
	return append(s, t...)
}

// Copy makes a new slice with copied elements.
func Copy[T any](s []T) []T {
	dst := make([]T, len(s))
	copy(dst, s)
	return dst
}

// Clear resets a slice to empty.
func Clear[T any](s []T) []T {
	return s[:0]
}

	
     **Map (Hash Map / Dictionary)**
	ages := map[string]int{
	    "Kiran":  35,
    	    "Arjun":  28,
	}
     **Struct**
	type Person struct {
    		Name string
		Age  int
	}
	p := Person{Name: "Kiran", Age: 35}
	or
	p := Person{"Kiran",35}
** Pointer**
x := 10
ptr := &x
fmt.Println(*ptr) 
**String**
s := "GoLang"
fmt.Println(s[0], string(s[0]))
Reverse String
s := "GoLang"
runes := []rune(s)
for i, j := 0, len(runes)-1; i < j; i, j = i+1, j-1 {
    runes[i], runes[j] = runes[j], runes[i]
}
fmt.Println(string(runes)) // gnaLoG
l

Use make for slices, maps, channels.
Use new rarely (low-level memory allocation).
Use var or literals for everything else.

## Panic
   Break the flow its kind of system.exit in java
   we can recover panic by deffer
	func risky() {
    		defer func() {
       		 if r := recover(); r != nil {
            		fmt.Println("Recovered from:", r)
        	 }
    	}()
    
    	panic("unexpected error")
	}
## Error
	* we can throw error .It will brak flow not exit flow
	func divide(a, b int) (int, error) {
   	 if b == 0 {
        	return 0, errors.New("cannot divide by zero")
   	 }
    	return a / b, nil
	}
## Chanels
	A channel is like a pipe between goroutines.
	One goroutine sends data, another receives it.
	Ensures synchronization → sender waits until data is received (for unbuffered channels).

	ch:=make(chan int)
	ch<- 42 //Send data to chan
	data:=<-ch //Receve data from changel
	