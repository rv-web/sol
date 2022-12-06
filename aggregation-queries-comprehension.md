# aggregation-queries

1. Returns a dictionary which maps each country code to the corresponding country.

    ```python
    def get_countries_by_codes(self) -> dict[str, Country]:
        return {
            country.code: country
            for country in self.countries
        }
    ```

1. Returns a dictionary which maps each region to the count of its countries.

    ```python
    def get_count_of_countries_by_regions(self) -> dict[Country.Region, int]:
        return {
            region: len([
                country
                for country in self.countries
                if country.region == region
            ])
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

1. Returns a dictionary which maps each region to its countries.

    ```python
    def get_countries_by_regions(self) -> dict[Country.Region, set[Country]]:
        return {
            region: {
                country
                for country in self.countries
                if country.region == region
            }
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

1. Returns a dictionary which maps each region to its most populous country.


    ```python
    def get_most_populous_country_by_regions(self) -> dict[Country.Region, Country]:
        return {
            region: next(
                country
                for country in self.countries
                if country.region == region and country.population == max(
                    {
                        country.population
                        for country in self.countries
                        if country.region == region
                    }
                )
            )
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

1. Returns a dictionary which maps each region the list of its countries ordered by their capital names to their continent.

    ```python
    def get_countries_by_regions_order_by_capitals(self) -> dict[Country.Region, list[Country]]:
        return {
            region: sorted(
                [
                    country
                    for country in self.countries
                    if country.region == region
                ],
                key=lambda country: country.capital
            )
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

1. Returns a dictionary which maps each region to the corresponding countries which population is between the given bounds (inclusive) to their continent.

    ```python
    def get_countries_by_regions_filter_by_population(self, lower_bound: int,
                                                      upper_bound: int) -> dict[Country.Region, set[Country]]:

        return {
            region: sorted(
                [
                    country
                    for country in self.countries
                    if country.region == region and lower_bound <= country.population <= upper_bound
                ],
                key=lambda country: country.capital
            )
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

3. Returns a dictionary which maps each region to the corresponding country codes, then each country code to the corresponding country.

    ```python
    def get_countries_by_regions_and_codes(self) -> dict[Country.Region, dict[str, Country]]:
        return {
            region: {
                country.code: country
                for country in self.countries
                if country.region == region
            }
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

4. Returns a dictionary which maps region to the letters that occur in the first place of corresponding country names, then each letter to the corresponding countries.

    ```python
    def get_countries_by_regions_and_first_letters(self) -> dict[Country.Region, dict[str, set[Country]]]:
        return {
            region: {
                letter: [
                    country
                    for country in self.countries
                    if country.region == region and country.name[0] == letter
                ]
                for letter in {
                    country.name[0]
                    for country in self.countries
                    if country.region == region
                }
            }
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

5. Returns a dictionary which maps the letters that occur in the first place of corresponding country names to regions, then each letter to the corresponding countries.

    ```python
    def get_countries_by_first_letters_and_regions(self) -> dict[str, dict[Country.Region, set[Country]]]:
        return {
            letter: {
                region: [
                    country
                    for country in self.countries
                    if country.region == region and country.name[0] == letter
                ]
                for region in {
                    country.region
                    for country in self.countries
                    if country.name[0] == letter
                }
            }
            for letter in {
                country.name[0]
                for country in self.countries
            }
        }
    ```

6. Returns a dictionary which maps each region to the set of country names, using the given locale.

    ```python
    def get_localized_country_names_by_regions(self, locale: str) -> dict[Country.Region, set[str]]:
        return {
            region: {
                country.translations[locale]
                for country in self.countries
                if country.region == region
            }
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

7. Returns a dictionary which maps each region to the country name which is the first in the given locale.

    ```python
    def get_first_localized_country_names_by_regions(self, locale: str) -> dict[Country.Region, str]:
        return {
            region: next(
                country.name
                for country in self.countries
                if country.region == region and locale in country.translations
            )
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```

8. Returns a dictionary which maps each region to the country which name is the first in the given locale.

    ```python
    def get_first_localized_countries_by_regions(self, locale: str) -> dict[Country.Region, Country]:
        return {
            region: next(
                country
                for country in self.countries
                if country.region == region and locale in country.translations
            )
            for region in {
                country.region
                for country in self.countries
            }
        }
    ```