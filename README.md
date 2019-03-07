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
This table contains information on the palaeomagnetic result, e.g. result,
laboratory tests, tilt correction, reversals, comments, etc. Its COLUMNS
include

* RESULT:

  * RESULTNO (4 digit primary key to link with ALTRESULT, FIELDTESTS and
    CROSSREF tables),

  * ROCKUNITNO (4 digit primary key to link with ROCKUNIT table),

  * COMPONENT (Name given by the author where several magnetisation components
    are identified. If the result is a combined pole the field will read
    'Combined result' and further details will be given in the COMMENTS field),

  * LOMAGAGE (or LOWMAGAGE, lower best estimate of the magnetic age of the
    magnetisation component),

  * HIMAGAGE (or HIGHMAGAGE, upper best estimate of the magnetic age of the
    magnetisation component),

  * TESTS (Various stability tests, designated by the following symbols R
    [Reversals test with subscripts a,b,c - see documentation;
    Ra,Rb,Rc,Rai,Rbi,Rci - see McFadden, 1990], M [Rock magnetic tests], C
    [baked contact test], C* [inverse contact test], G [conglomerate test], G*
    [intraformational conglomerate test]. F [fold test, also called tilt test
    or bedding-tilt test], F* [synfold test], Fs [fold test + strain removal],
    Details of field tests are given in the FIELDTEST table. U [Unconformity
    test (after Kirschvink)], N [no tests], where "+", "-" or "o" are used to
    indicate positive, negative or inconclusive 不确定的 tests),

  * TILT (Percentage tilt correction applied [usually 0 or 100, except synfold]),

  * SLAT (Latitude of site position for calculating the pole position),

  * SLONG (Longitude of site position for calculating the pole position; lies in
    the range -180.0 to +180.0),

  * The usual directional parameters:

    * B (Number of sites),
    * N (Number of samples),
    * DEC (Remanence Declination east of true north 磁偏角),
    * INC (Remanence Inclination, i.e. Inclination of mean direction of
      magnetization 磁倾角),
    * KD (Fisher precision parameter for mean direction),
    * ED95 (Radius of Circle of 95% confidence about mean direction, i.e.
      \alpha95),

  * PLAT (Latitude of Paleomagnetic Pole [VGP] Position),

  * PLONG (Longitude of Paleomagnetic Pole [VGP] Position; in the range 0.0 to
    360.0),

  * PTYPE (How the pole was calculated: D indicates pole calculated from mean
    DEC,INC; V indicates pole calculated from VGPs [mean VGP] [in this case
    DP=DM=EP95]),

  * Error parameters on the pole position (in degrees):

    * DP (half-angle of the confidence on the VGP in the direction of the
      palaeomeridian, i.e. semi-axis of oval of 95% confidence about Pole
      Position),
    * DM (half-angle of the confidence on the VGP perpendicular to the
      palaeomeridian, i.e. the other semi-axis of oval of 95% confidence about
      Pole Position),

  * NOREVERSED (Percent of Reversed polarity data, i.e. directions of
    magnetization),

* REVERSALS:

  * ANTIPODAL (Angle between the mean Normal and mean Reversed direction
    results),

  * Directional parameters for the normal polarity results:

    * N_NORM (Number of Normal directions),
    * D_NORM (Declination of mean Normal directions),
    * I_NORM (Inclination of mean Normal directions),
    * K_NORM (Fisher precision parameter for Normal directions),
    * ED_NORM (Circle of 95% confidence about Normal directions),

  * Directional parameters for the reversed polarity results:

    * N_REV (Number of Reversed directions),
    * D_REV (Declination of mean Reversed directions),
    * I_REV (Inclination of mean Reversed directions),
    * K_REV (Fisher precision parameter for Reversed directions),
    * ED_REV (Circle of 95% confidence about Reversed directions),

* LABORATORY TESTS:

  * DEMAGCODE (Number in the range 0-5 describing cleaning procedures used).
    Laboratory analytical procedures:

    * 0 = No demagnetisation
    * 1 = Only pilot demagnetisation on some samples
    * 2 = All samples treated, blanket treatment only
    * 3 = Stereonets with J/Jo, or vector plots provided
    * 4 = Principal component analysis (PCA) plus vector or stereoplots and J/Jo
    * 5 = PCA plus multiple treatments that successfully isolate components of
      magnetisation (e.g. alternating field (AF) and Thermal or Thermal and
      Chemical)

  * TREATMENT 退磁处理方法 (Demagnetisation Treatment with symbols A
    [AF treatment], T [thermal treatment], H [chemical treatment], N [no
    demagnetisation treatment], V indicates temporary cleaning used (Soviet
    Data)),

  * LABDETAILS (Information such as maximum AF field or temperature used for
    pilot test purposes),

  * ROCKMAG (Summary of basic rock magnetic data studies, with symbols OP
    [Opaques from reflected light where MAGN = magnetite, MAGH = maghemite, TM =
    titanomagnetite, TMH = titanomaghemite, ILM = ilmenite, HEM = hematite, THEM
    = titanohematite, GEOTH = geothite, PYRR = pyrrhotite, RUT = rutile, MART =
    martite], Js-T [Thermomagnetic saturation magnetization vs temperature data;
    Curie temperatures], IRM [Isothermal remanent magnetization acquisition
    (with saturation field)], SUSC [Susceptibility], AN [Anisotropy; Anisotropy
    of MS: 不同方向上的磁化能力不同.], Hc [Coercivity of remanence] etc),

* TILT CORRECTION:

  * N_TILT (Number of measurements used for means before and after structural
    correction),

  * Directional parameters before tilt correction:

    * D_UNCOR (Declination before correction for structure),
    * I_UNCOR (Inclination before correction for structure),
    * K1 (Fisher precision parameter before structure correction),
    * ED1 (Circle of 95% confidence before structural correction),

  * Directional parameters after tilt correction:

    * D_COR (Declination after correction for structure),
    * I_COR (Inclination after correction for structure),
    * K2 (Fisher precision parameter after structure correction),
    * ED2 (Circle of 95% confidence after structural correction),

* COMMENTS:

  * COMMENTS (General information including details of the origin of MAGAGE.
    If the result is a combined pole this field contains information on the data
    included in the combined result)

  * STATUS (Indicates if results have been superseded). Notes on the status of
    the result:

    * 'Superseded by...' = the result is superseded by another in the database
    * 'Old result' = the result is old with very limited laboratory analysis
    * 'Data included in...' = the result is included in a combined pole
    * 'See...' = there is some reason to refer to another result in the database

#### ALTRESULT
This table contains palaeomagnetic results (alternative pole position)
calculated in a different way from the main PMAGRESULT table. Its COLUMNS are

* RESULTNO (link with PMAGRESULT table)

* Pole position and statistics when derived from a mean VGP (if this
  calculation is the only one given by the author then APLAT = PLAT, APLONG =
  PLONG and DP = DM = EP95 from the PMAGRESULT table):
  * APLAT (Pole Latitude calculated from the mean VGP)
  * APLONG (Pole Longitude calculated from the mean VGP)
  * KP (Fisher precision parameter for mean VGP; Watch [this video][1] showing
    how dispersion behaves for different Fisher precision parameter)
  * EP95 (A95? Radius of circle of 95% confidence about Pole position; see Tauxe
    et al. 2005 Chp 7; Domeier et al. 2012)


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

* CONTINENT (in GPMDB4.6b, it was one of 12 present-day continents; here it is
  one of plates/blocks/terranes in east asia or even broader area),

* TERRANE (Terrane name where this has been mentioned by the author),

* RLAT (Latitude of the rockunit),

* RLONG (Longitude of the rockunit),

* ROCKTYPE (One of four possible rock types),

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

1. Part of the definitions of the above terms is from the website http://www.ngu.no/geodynamics/gpmdb/,
   which is now closed.

[1]: https://youtu.be/hu-3U-jSQME
