# Paleomagnetic_Data_from_Chinese_Literature (暂用此命名该数据库)
This database is a compilation of paleomagnetic data from Chinese literature.
It is created using Structured Query Language (SQL). I'm using an open source
database engine SQLite (version 3.x.x) to manage it.

该数据库收集归纳中文文献里发表的古地磁极数据。数据库的创建和管理基于SQL语言。我
这里用的是开源SQL数据库管理软件包SQLite。

## Why Do It (创建该数据库的缘由)
Many paleomagnetic data were published only in Chinese. So why not share them
with a "Hello, World!".

在我读硕士期间，科研涉及到很多塔里木板块的板块构造历史和古地磁数据。当时我发现很
多古地磁数据（当然应该是100%关于中国范围内的板块、地块、地体的古地磁）是发表在中
文学术期刊内的，因此未能被归纳到GPMDB（英文世界里的“全球古地磁数据库”）。我觉得这
样没能和世界分享挺可惜的，所以才有了这个想法，但至今才得以实施。

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
include

* ROCKUNITNO (4 digit primary key to link ROCKUNIT and PMAGRESULT),

* RESULTNO (4 digit primary key to link PMAGRESULT, ALTRESULT etc),

* LOMAGAGE (),

* HIMAGAGE (),

* TESTS (Various stability tests symbols R [Reversals test with subscripts
  a,b,c - see documentation], M [Rock magnetic tests], C [baked contact test],
  C* [inverse contact test], G [conglomerate test], G* [intraformational
  conglomerate test], F [fold test], F* [synfold test], Fs [fold test + strain
  removal], U [Unconformity test], N [no tests]),

* TILT (Percent tilt correction [usually 0 or 100, except synfold]),

* SLAT (Latitude of site position for calculating the pole position),

* SLONG (Longitude of site position for calculating the pole position; lies in
  the range -180.0 to +180.0),

* B (Number of sites),

* N (Number of samples),

* DEC (Remanence Declination east of true north 磁偏角),

* INC (Remanence Inclination, i.e. Inclination of mean direction of
  magnetization 磁倾角),

* KD (Fisher precision parameter for mean direction),

* ED95 (Radius of Circle of 95% confidence about mean direction, i.e. \alpha95),

* PLAT (Latitude of Paleomagnetic Pole [VGP] Position),

* PLONG (Longitude of Paleomagnetic Pole [VGP] Position; in the range 0.0 to
  360.0),

* PTYPE (How the pole was calculated: D=pole calculated from mean DEC,INC;
  V=pole calculated from VGPs [mean VGP] [in this case DP = DM = EP95]),

* DP (half-angle of the confidence on the VGP in the direction of the
  palaeomeridian, i.e. semi-axis of oval of 95% confidence about Pole Position),

* DM (half-angle of the confidence on the VGP perpendicular to the
  palaeomeridian, i.e. the other semi-axis of oval of 95% confidence about Pole
  Position),

* NOREVERSED (Percent of Reversed directions of magnetization),

* ANTIPODAL (Angle between the mean Normal and mean Reversed directions),

* N_NORM (Number of Normal directions),

* N_REV (Number of Reversed directions),

* D_NORM (Declination of mean Normal directions),

* I_NORM (Inclination of mean Normal directions),

* K_NORM (Fisher precision parameter for Normal directions),

* ED_NORM (Circle of 95% confidence about Normal directions),

* D_REV (Declination of mean Reversed directions),

* I_REV (Inclination of mean Reversed directions),

* K_REV (Fisher precision parameter for Reversed directions),

* ED_REV (Circle of 95% confidence about Reversed directions),

* DEMAGCODE (Number in the range 0-5 describing cleaning procedures used),

* TREATMENT (Treatment with symbols A [alternating field treatment], T [thermal
  treatment], H [chemical treatment], N [no treatment]),

* LABDETAILS,

* ROCKMAG (Rock magnetic data with symbols OP [Opaques from reflected light],
  Js-T [Thermomagnetic saturation magnetization vs temperature data],
  IRM [Isothermal remanent magnetization (with saturation field)],
  SUSC [Susceptibility], AN [Anisotropy], Hc [Coercivity of remanence] etc),

* N_TILT (Number used for means before and after structural correction),

* D_UNCOR (Declination before correction for structure),

* I_UNCOR (Inclination before correction for structure),

* K1 (Fisher precision parameter before structure correction),

* ED1, ED2 (Circle of 95% confidence before, after structural correction),

* D_COR (Declination after correction for structure),

* I_COR (Inclination after correction for structure),

* K2 (Fisher precision parameter after structure correction),

* STATUS (Indicates if results have been superseded),

* COMPONENT, COMMENTS

#### REFERENCE
This table contains information on the literature where the palaeomagnetic data
was published. Its COLUMNS include

* REFNO (In GPMDB4.6b, it is 4 digit primary key to link AUTHORS, REFERENCE, and
  ROCKUNIT; For the data compiled here it becomes 6 digit primary key to link
  AUTHORS, REFERENCE, ROCKUNIT, and its first 2 digits are always 8 and 6, which
  is named after China's country code 86),

* AUTHORS,

* AUTHORS_cn (Authors' names in Chinese),

* YEAR,

* VOLUME,

* TITLE,

* TITLE_cn (Title in Chinese),

* REMARKS,

* VPAGES,

* JOURNAL,

* JOURNAL_cn (Journal name in Chinese)

#### ROCKUNIT
This table contains information on the sampled rockunit, e.g. position, geology,
age, structure. Its COLUMNS include:

* REFNO (link with REFERENCE table),

* ROCKUNITNO (link with PMAGRESULT table),

* ROCKNAME (Rock name),

* PLACE (Location of investigation including name of country),

* CONTINENT,

* TERRANE,

* RLAT (Latitude of the rockunit),

* RLONG (Longitude of the rockunit),

* ROCKTYPE,

* STRATA (Stratigraphic information such as "Visean"),

* STRATAGE (Stratigraphic age using common symbols as listed in TIMESCALE table),

* LATSPREAD (Latitudinal spread of rock unit),

* LOWAGE (Numerical lower age limit),

* HIGHAGE (Numerical upper age limit),

* METHOD (Basis upon which LOWAGE and HIGHAGE values have been derived),

* STATUS (Indicates the results have been superseded),

* ISOTOPEDATA (Isotopic age information),

* STRUCTURE (Comments on strikes and dips of bedding or the age of folding or
  metamorphism)

#### TERRANE
This table contains information on terrane name which has been mentioned by
the author, and also the corresponding continent where the terrane is located.
So its COLUMNS include CONTINENT and TERRANE.

## References

1. Part of the definitions of the above terms is from http://www.ngu.no/geodynamics/gpmdb/ (please note that this website is down
   now)
