# Paleomagnetic_Data_from_Chinese_Literature
This database is a compilation of paleomagnetic data from Chinese literature.
It is created using Structured Query Language (SQL). I'm using an open source
database engine SQLite (version 3.x.x) to manage it.

## Why Do It
Many paleomagnetic data were published only in Chinese. So why not share them
with a "Hello, World!".

## Initial Idea
This small database will include two versions. One contains data from the
literature published only in Chinese. The other one contains all the data
published in English or Chinese for those tectonic plates/blocks/terranes of
East Asia, mainly China area, for example, North China, South China, Tarim, etc.

## Format
I'm referring to GPMDB4.6b's schema. Please [click here][1] for more details
about GPMDB4.6b.

[1]: https://confluence.csiro.au/display/cmfr/Palaeomagnetism+and+Rock+Magnetism

### Tables
#### PMAGRESULT
This table contains information on the palaeomagnetic result. Its COLUMNS
include ROCKUNITNO, RESULTNO, LOMAGAGE, HIMAGAGE, TESTS, TILT, SLAT, SLONG, B,
N, DEC, INC, KD, ED95, PLAT, PLONG, PTYPE, DP, DM, NOREVERSED, ANTIPODAL,
N_NORM, D_NORM, I_NORM, K_NORM, ED_NORM, N_REV, D_REV, I_REV, K_REV, ED_REV,
DEMAGCODE, TREATMENT, LABDETAILS, ROCKMAG, N_TILT, D_UNCOR, I_UNCOR, K1, ED1,
D_COR, I_COR, K2, ED2, STATUS, COMPONENT, COMMENTS

#### REFERENCE
This table contains information on the literature where the palaeomagnetic data
was published. Its COLUMNS include

REFNO (In GPMDB4.6b, it is 4 digit primary key to link AUTHORS, REFERENCE, ROCKUNIT; Here it is 6 digit primary key to link AUTHORS, REFERENCE, ROCKUNIT, and its first 2 digits are always 86, which is named after China's country code 86),

AUTHORS, AUTHORS_cn, YEAR, VOLUME,
TITLE, TITLE_cn, REMARKS, VPAGES, JOURNAL, JOURNAL_cn

#### TERRANE
This table contains information on terrane name which has been mentioned by
the author, and also the corresponding continent where the terrane is located.
So its COLUMNS include CONTINENT and TERRANE.
