# Music array notation

A simple format to represent pitch classes, intervals and notes.

The aim of this specification is to create a simple and string-independent format to exchange pitch information among different libraries.

This is the internal pitch format for [music.kit](https://www.npmjs.com/package/music.kit) javascript library. __You don't need to know this to use the library__. This document is for library builders only.

## Features

- Can represent different types of pitched elements
- All numerical, no need to parse
- All entities represented by an array
- The array length determine the type of the element

## Encoding

### 1. Pitch classes

A pitch class is a note name without octave (letter and accidentals).

A pitch class is encoded using a 1-element array in the format `[ fifhts ]` where:

- __fifths__ `{Integer}`: the number of fifths from C to the pitch class.

Here are the unaltered pitch classes in array notation:

| C | D | E | F | G | A | B |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| ` [0] `| ` [2] `| ` [4] `| ` [-1] `| ` [1] `| ` [3] `| ` [5] `|

Add 7 to add sharps:

| C# | D# | E# | F# | G# | A# | B# |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| ` [7] ` | ` [9] ` | ` [11] ` | ` [6] ` | ` [8] ` | ` [10] ` | ` [12] ` |


Subtract 7 to add flats:

| Cb | Db | Eb | Fb | Gb | Ab | Bb |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| ` [-7] ` | ` [-5] ` | ` [-3] ` | ` [-8] ` | ` [-6] ` | ` [-4] ` | ` [-2] ` |

### 2. Intervals

Intervals are encoded by 2-element arrays with the form `[ fifths, octaves ]` where:

- __fifths__ `{Integer}`: the number of fifths (same as pitch class)
- __octaves__ `{Integer}`: is the number of octaves (positive are ascending, negative descending)

For example, a major second is two fifths up and one octave down: `[2, -1]`


Here are the most popular ascending intervals:

| Interval name | Short | Array notation |
| :-- | :-: | :-: |
| unison | 1P | `[0, 0]` |
| minor second | 2m | `[-5, 3]` |
| major second | 2M | `[2, -1]` |
| minor third | 3m | `[-3, 2]` |
| major third | 3M | `[4, -3]` |
| perfect fourth | 4P | `[-1, 1]` |
| augmented fourth | 4A | `[6, -3]` |
| diminished fifth | 5d | `[-6, 4]` |
| perfect fifth | 5P | `[1, 0]` |
| minor sixth | 6m | `[-4, 3]` |
| major sixth | 6M | `[3, -2]` |
| minor seven | 7m | `[-2, 2]` |
| major seven | 7M | `[5, -2]` |
| octave | 8P | `[0, 1]` |

Compound intervals are created by adding octaves:

| Simple | | Compound | |
| :-- | :-: | :-: |
| second | `[2, -1]` | ninth | `[-2, 0]`
| third | `[4, -3]` | tenth | `[4, -2]`
| ... | ... | ... | ... |


Descending intervals are the same as ascending but with opposite direction:

| Interval | Ascending | Descending |
| :-- | :-: | :-: |
| major second | `[2, -1]` | `[-2, 1]`
| major third | `[4, -3]` | `[-4, 3]`
| .... | | ||

### 3. Pitches and notes

For pitches and notes, a 3-length array is used with the form `[fifths, octaves, duration]` where:

- __fifths__ `{Integer}`: number of fifths
- __octaves__ `{Integer}`: number of octaves
- __duration__ `{Integer}`: the duration of the note. Can be `null` to represent pure pitches (notes without duration).

Duration has no defined value, its only a relative duration where an outside reference is needed to convert to time units. Popular choices are 96 or 720 to represent quarter notes.

## Resources and inspiration

This format is largely based on the `coord` format of [teoria](https://github.com/saebekassebil/teoria), that is based on the discontinued music theory framework [music.js](http://www.gregjopa.com/2011/05/calculate-note-frequencies-in-javascript-with-music-js/)

## License

MIT License
