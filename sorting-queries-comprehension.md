# sorting-queries

1. Returns the list of countries ordered by:

   * their populations in descending order

    ```python
    def get_countries_order_by_population_desc(self) -> list[Country]:
        return sorted(
            self.countries,
            key=lambda country: -country.population
        )
    ```

2. Returns the list of countries ordered by:

   * the names of their capitals
   * their population in descending order

    ```python
    def get_countries_order_by_length_of_capital_then_by_population_desc(self) -> list[Country]:
        return sorted(
            self.countries,
            key=lambda country: (len(country.capital), -country.population)
        )
    ```

3. Returns the list of countries ordered by:

   * the length of the names of their capitals
   * their capitals

    ```python
    def get_countries_order_by_length_of_capital_then_by_capital(self) -> list[Country]:
        return sorted(
            self.countries,
            key=lambda country: (len(country.capital), country.capital)
        )
    ```

4. Returns the capital of each country in descending order.

   ```python
   def get_capitals_order_by_name_desc(self) -> list[str]:
       return sorted(
           [
               country.capital
               for country in self.countries
           ],
           key=lambda country: country.name, reverse=True
       )
   ```
