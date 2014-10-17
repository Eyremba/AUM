	AUM - A minimal CSPRNG reflecting the Zen of cipher design.
	AUM is an AUM with a 16, 32 or 64 +4-word internal state
	AUM may be seeded with a 512-, 1024- or 2048-bit key
	AUM Copyright C.C.Kayne 2014, GNU GPL V.3, cckayne@gmail.com
	AUM is inspired by Bob Jenkins' PRNG insights (Public Domain).

What is AUM?

AUM is a fast, small-state, cryptographically secure pseudo-random number generator (CSPRNG) and stream cipher. AUM exhibits uniform distribution, mixes rapidly, has no detected bias, and comes in three variants: AUM16, with an internal state array of 16+4 32-bit words; AUM32, with an internal state of 32+4 words; and AUM64 with a 64+4-word state. The former permit seeding with a key of up to 512 or 1024 bits, the latter with a 2048-bit key.

Stripped to essentials, AUM is only 5 lines of code:

		e = a
		a = b ^ c
		b = c - d
		c = d + e
		d = e + a
		
<a> being indexes into AUM's internal state array.
		
Two additions, one subtraction, one XOR, two pseudo-random lookups. Six arithmetic and bitwise operations in all. It's called AUM - and pronounced 'OM' - because it best reflects the Zen of PRNG creation - everything superfluous peeled away, leaving just those six simple operations.

Mean avalanche between successive calls to AUM is an impressive 16 bits, with a 30-bit maximum. In other words, mixing efficiency is nearly optimal. 

The three AUM variants presented here have been implemented identically in C and Pascal and can be found in their respective directories along with a short program to check their output. AUM was developed and tested with the Microsoft Visual C compiler (cl) and Free Pascal (fpc) under Win32. The NIST statistical tests were run under Linux.

To view AUM's abbreviated internal state, please uncomment "#define TEST" in the C files and "{$define TEST}" in the Pascal files and "#define VERBOSE" and "{$define VERBOSE}" to display the full result & state arrays as they are generated on each call.

PRNG tests passed by AUM:

* NIST suite of statistical tests for randomness: all tests for all seeds
* George Marsaglia's DIEHARD suite: all tests for all seeds
* Bob Jenkins' countx for sub-sequences of length 2-12 (2**35 trials)
* John Walker's ENT test for entropy
* C.C.Kayne's GapTrial (value-spacings normal over all modulos)
* C.C.Kayne's ModTrial (value-distributions uniform over all modulos)
* C.C.Kayne's SeqTrial (same-value sequences normal over all modulos)
* C.C.Kayne's PopTrial (bit-populations iid-normal over all trial ranges)
* C.C.Kayne's Visual 1 & 2

(Please view the Results.txt files in the relevant folders or verify the recorded results by re-running the tests themselves. The principal AUM repositories are listed at the foot of this document.)


Why AUM?

For extensive background to the rationale behind the creation of AUM, please consult the essay "On Using PRNGs as the Basis for Stream Ciphers" included in this distribution. Briefly, AUM was originally designed as a base mixing unit for the plug-in of existing "non-cryptographic" RNGs and other random functions, but it soon emerged as an eminently serviceable CSPRNG in its own right, superior to several other related ciphers that were tested in parallel.

Have fun with AUM, and don't hesitate to get in touch if you encounter issues with any of the files included in this distribution. As always, your comments, suggestions, criticism and general feedback are welcomed.

C.C.Kayne
cckayne@gmail.com
https://github.com/cckayne/AUM
https://sourceforge.net/projects/aum-csprng-stream-cipher/
https://code.google.com/p/aum-csprng-stream-cipher/
https://code.google.com/p/bedbug-csprng-stream-cipher/
https://sourceforge.net/projects/bedbug-csprng-stream-cipher/
