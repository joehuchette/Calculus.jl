Calculus.jl
===========

[![Build Status](https://travis-ci.org/johnmyleswhite/Calculus.jl.svg?branch=master)](https://travis-ci.org/johnmyleswhite/Calculus.jl)
[![Calculus](http://pkg.julialang.org/badges/Calculus_release.svg)](http://pkg.julialang.org/?pkg=Calculus&ver=release)

# Introduction

The Calculus package provides tools for working with the basic calculus
operations of differentiation and integration. You can use the Calculus package to produce
approximate derivatives by several forms of finite differencing or to
produce exact derivative using symbolic differentiation.
You can also compute definite integrals by different numerical methods.

# API

Most users will want to work with a limited set of basic functions:

* `derivative()`: Use this for functions from R to R
* `second_derivative()`: Use this for functions from R to R
* `gradient()`: Use this for functions from R^n to R
* `hessian()`: Use this for functions from R^n to R
* `integrate()`: Use this to integrate functions from R to R
* `differentiate()`: Use this to perform symbolic differentiation
* `simplify()`: Use this to perform symbolic simplification
* `deparse()`: Use this to get usual infix representation of expressions

# Usage Examples

There are a few basic approaches to using the Calculus package:

* Use finite-differencing to evaluate the derivative at a specific point
* Use higher-order functions to create new functions that evaluate derivatives
* Use integration by Simpson's rule or Monte Carlo method to evaluate definite integrals
* Use symbolic differentiation to produce exact derivatives for simple functions

## Direct Finite Differencing

	using Calculus

	# Compare with cos(0.0)
	derivative(sin, 0.0)
	# Compare with cos(1.0)
	derivative(sin, 1.0)
	# Compare with cos(pi)
	derivative(sin, float64(pi))

	# Compare with [cos(0.0), -sin(0.0)]
	gradient(x -> sin(x[1]) + cos(x[2]), [0.0, 0.0])
	# Compare with [cos(1.0), -sin(1.0)]
	gradient(x -> sin(x[1]) + cos(x[2]), [1.0, 1.0])
	# Compare with [cos(pi), -sin(pi)]
	gradient(x -> sin(x[1]) + cos(x[2]), [float64(pi), float64(pi)])

	# Compare with -sin(0.0)
	second_derivative(sin, 0.0)
	# Compare with -sin(1.0)
	second_derivative(sin, 1.0)
	# Compare with -sin(pi)
	second_derivative(sin, float64(pi))

	# Compare with [-sin(0.0) 0.0; 0.0 -cos(0.0)]
	hessian(x -> sin(x[1]) + cos(x[2]), [0.0, 0.0])
	# Compare with [-sin(1.0) 0.0; 0.0 -cos(1.0)]
	hessian(x -> sin(x[1]) + cos(x[2]), [1.0, 1.0])
	# Compare with [-sin(pi) 0.0; 0.0 -cos(pi)]
	hessian(x -> sin(x[1]) + cos(x[2]), [float64(pi), float64(pi)])

## Higher-Order Functions

	using Calculus

	g1 = derivative(sin)
	g1(0.0)
	g1(1.0)
	g1(pi)

	g2 = gradient(x -> sin(x[1]) + cos(x[2]))
	g2([0.0, 0.0])
	g2([1.0, 1.0])
	g2([pi, pi])

	h1 = second_derivative(sin)
	h1(0.0)
	h1(1.0)
	h1(pi)

	h2 = hessian(x -> sin(x[1]) + cos(x[2]))
	h2([0.0, 0.0])
	h2([1.0, 1.0])
	h2([pi, pi])

## Prime Notation

For scalar functions that map R to R, you can use the `'` operator to calculate
derivatives as well. This operator can be used abritratily many times, but you
should keep in mind that the approximation degrades with each approximate
derivative you calculate:

	using Calculus

	f(x) = sin(x)
	f'(1.0) - cos(1.0)
	f''(1.0) - (-sin(1.0))
	f'''(1.0) - (-cos(1.0))

## Integration using Simpson's Rule

	using Calculus

	# Compare with log(2)
	integrate(x -> 1 / x, 1.0, 2.0)

	# Compare with cos(pi) - cos(0)
	integrate(x -> -sin(x), 0.0, float64(pi))

## Integration using Monte Carlo method

	using Calculus

	# Compare with cos(pi) - cos(0)
	integrate(x -> -sin(x), 0.0, float64(pi), :monte_carlo)

## Symbolic Differentiation

	using Calculus

	differentiate("cos(x) + sin(x) + exp(-x) * cos(x)", :x)
	differentiate("cos(x) + sin(y) + exp(-x) * cos(y)", [:x, :y])

# Coming Soon

* Finite differencing based on complex numbers

# Credits

Calculus.jl is built on contributions from:

* John Myles White
* Tim Holy
* Andreas Noack Jensen
* Nathaniel Daw
* Blake Johnson
* Avik Sengupta

And draws inspiration and ideas from:

* Mark Schmidt
* Jonas Rauch
