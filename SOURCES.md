# Data sources and preparation

The listing records come from [Inside Airbnb](https://insideairbnb.com/get-the-data/),
an independent project that collects publicly available Airbnb listing data.
Data are provided under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

| Market | Detailed source snapshot | Record collection dates | Rows in airbnb.csv |
| --- | --- | --- | ---: |
| Denver | [September 25, 2026 directory](https://data.insideairbnb.com/united-states/co/denver/2026-09-25/data/listings.csv.gz) | September 28-29, 2026 | 1,717 |
| Seattle | [September 20, 2026 directory](https://data.insideairbnb.com/united-states/wa/seattle/2026-09-20/data/listings.csv.gz) | September 21-22, 2026 | 3,120 |
| Portland | [September 14, 2026 directory](https://data.insideairbnb.com/united-states/or/portland/2026-09-14/data/listings.csv.gz) | September 14, 2026 | 1,685 |

The extract retains entire homes and private rooms with advertised minimum
stays of one to seven nights. One listing was randomly selected per host within
each market. Client properties and their hosts are excluded from the market
file. Project listing identifiers replace source identifiers.

Selected source variables were renamed using lowercase letters and underscores.
Prices were converted from currency text to numbers, bathroom counts were parsed
from listing descriptions, and Superhost status was labeled Yes or No. The
original detailed property categories and full advertised amenity lists were
retained. `checkin_month` is the month of `price_quote_checkin_date`, coded
1 (January) through 12 (December); missing dates remain blank.
Missing values remain blank; no prices were trimmed or winsorized and
no artificial missing or nonsense values were added.

The amenity indicators are derived from the advertised list, ignoring case:

- `pets_allowed`: the list includes `Pets allowed`.
- `free_parking_on_premises`: an item starts with `free ` and contains both
  `parking` and `on premises`, including driveway and garage variants.
- `free_street_parking`: the list includes `Free street parking`.
- `air_conditioning`: an item contains `air conditioning`, including central
  and portable variants.

No means not advertised in the list, rather than independently verified absence.
A missing amenity list produces blank indicators. An empty list produces No.
Listings can advertise both types of parking.

The price is the advertised price per night in US dollars for the stay quoted
when the data was collected. It is not realized booking revenue. The client file has
the same variable definitions, except that the price column is omitted.
