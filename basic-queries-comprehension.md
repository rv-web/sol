# basic-queries

1. Returns the value of the greatest population.

    ```python
    def get_greatest_population(self) -> int:
        return max({
            country.population 
            for country in self.countries
        })
    ```

2. Returns the value of the average population.

    ```python
    def get_average_population(self) -> float:
        return sum([
            country.population 
            for country in self.countries
        ]) / float(len(self.countries))
    ```

3. Returns the count of European countries.

    ```python
    def get_count_of_european_countries(self) -> int:
        return len([
            country
            for country in self.countries
            if country.region == Country.Region.EUROPE
        ])
    ```

4. Returns the count of countries that are located in the given continent.

    ```python
    def get_count_of_countries_of_region(self, region: Country.Region) -> int:
        return len([
            country 
            for country in self.countries 
            if country.region == region
        ])
    ```

5. Returns the population of the given continent.

    ```python
    def get_population_by_region(self, region: Country.Region) -> int:
        return sum([
            country.population
            for country in self.countries
            if country.region == region
        ])
    ```

6. Returns whether a country exists having the given population.

    ```python
    def is_population_exists(self, population: int) -> bool:
        return bool([
            country
            for country in self.countries
            if country.population == population
        ])
    ```

7. Returns the country which has the given code.

    ```python
    def get_country_by_code(self, code: str) -> Optional[Country]:
        return next(
            country
            for country in self.countries
            if country.code == code
        )
    ```

8. Returns the country which has the greatest population of its continent.

    ```python
    def get_most_populous_country_by_region(self, region: Country.Region) -> Country:
        max_population = max([
            country.population
            for country in self.countries
            if country.region == region
        ])

        return next(
            country
            for country in self.countries
            if country.region == region and country.population == max_population
        )
    ```

9. Returns the first country which name starts with the given letter.

    ```python
    def get_first_country_by_starting_letter(self, letter: str) -> Optional[Country]:
        return next(
            country
            for country in self.countries
            if country.name[0] == letter
        )
    ```

10. Returns a set containing all the distinct country names.

    ```python
    def get_distinct_names(self) -> set[str]:
        return {
            country.name 
            for country in self.countries
        }
    ```

11. Returns a set containing all the distinct capitals.

    ```python
    def get_distinct_capitals(self) -> set[str]:
        return {
            country.capital
            for country in self.countries
        }
    ```

12. Returns the set of countries which population is less than the given limit.

    ```python
    def get_countries_below_population_limit(self, limit: int) -> set[Country]:
        return {
            country 
            for country in self.countries 
            if country.population < limit
        }
    ```

13. Returns all the population values that belong to the given continent.

    ```python
    def get_distinct_populations_by_region(self, region: Country.Region) -> set[int]:
        return {
            country.population
            for country in self.countries
            if country.region == region
        }
    ```

14. Returns each country which has a population which is between the given bounds (inclusive).

    ```python
    def get_countries_by_population(self, lower_bound: int, upper_bound: int = None) -> set[Country]:
        return {
            country
            for country in self.countries
            if lower_bound <= country.population and (country.population <= upper_bound if upper_bound else True)
        }