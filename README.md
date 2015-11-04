# Music array notation

A simple format to represent pitch classes, intervals and notes.

The aim of this specification is to create a simple and string-independent format to exchange pitch information among different libraries.

## Features

- Can represent different kind of pitched elements
- Numerical, no need to parse
- All entities represented by an array
- The array length determine the type of the entity.

## Encoding

### 1. Pitch classes

A pitch class is a note name without octave (letter and accidentals).

A pitch class is encoded using a 1-element array with an integer.

- `[0] {Integer}` __fifths__: the number of fifths from F to the pitch class.

Here are the basic pitch classes and in array notation:

| C | D | E | F | G | A | B |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| ` [1] `| ` [3] `| ` [5] `| ` [0] `| ` [2] `| ` [4] `| ` [6] `|

Going up an octave means add a sharp:

| C# | D# | E# | F# | G# | A# | B# |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| ` [8] ` | ` [10] ` | ` [12] ` | ` [7] ` | ` [9] ` | ` [11] ` | ` [13] ` |

For each octave up, you add a sharp.

Going octaves down is for flats:

| Cb | Db | Eb | Fb | Gb | Ab | Bb |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| ` [-6] ` | ` [-4] ` | ` [-2] ` | ` [-7] ` | ` [-5] ` | ` [-3] ` | ` [-1] ` |

The general rule is: `pitch class number = indexOf('FCDEGAB') + 7 * alteration` where alteration is 0 for no accidentals, +1 for sharps, -1 for flats.

### 2. Intervals

For intervals a 2-element array is used:

- `[0] {Integer}` __fifths__: the number of fifths (same as pitch class)
- `[1] {Integer}` __octaves__: is the number of octaves.


For example, a major second is two fifths up and one octave down: `[2, -1]`


Here are the most popular ascending intervals:

| Interval name | Short | Array notation |
| :-- | :-: | :-: |
| unison | 1P | `[0, 0]` |
| major second | 2M | `[2, -1]` |
| major third | 3M | `[4, -3]` |
| perfect fourth | 4P | `[-1, 1]` |
| perfect fifth | 5P | `[1, 0]` |
| major sixth | 6M | `[3, -2]` |
| minor seven | 7m | `[0, 0]` |
| major seven | 7M | `[0, 0]` |

#### Descending intervals



### 3. Pitches and notes

For pitches and notes, a 3-length array is used:

- `[0] {Integer}` __fifths__: number of fifths
- `[1] {Integer}` __octaves__: number of octaves
- `[2] {Object}` __duration__: the duration of the note. Can be `null` to represent pure pitches (notes without duration)

The duration can be represented with integers or with any other object (strings, ...)

## Resources and inspiration

This format is largely based on the `coord` format of [teoria](https://github.com/saebekassebil/teoria)

## License

MIT License
