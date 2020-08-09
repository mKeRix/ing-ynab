# ing_ynab [![lint](https://github.com/bahlo/fints_ynab/workflows/lint/badge.svg)](https://github.com/bahlo/ing_ynab/actions?query=workflow%3Alint) [![docker](https://github.com/bahlo/ing_ynab/workflows/docker/badge.svg)](https://github.com/bahlo/ing_ynab/actions?query=workflow%3Adocker)

Import your ING (de) bank statements via FinTS into YNAB. 

## Usage

This application will import your bank statements in a predefined interval 
(defaults to 5 minutes). 
You need to [register your FinTS product](https://www.hbci-zka.de/register/prod_register.htm) 
to get a product ID. 
If you don't do this, you might get blocked by your bank (as it defaults to the
one from the [python-fints](https://python-fints.readthedocs.io) library).

### Local

1. `pip install pipenv` to install [pipenv](https://pipenv.pypa.io) 
2. `pipenv shell` to spawn a new shell with your env
3. `pipenv install` to install dependencies
4. `cp .env.example .env` and customize fields
5. `python ing_ynab`

### Docker

1. `cp .env.example .env` and customize fields
2. `docker run -v $PWD/state:/app/state --env-file .env docker.pkg.github.com/bahlo/ing_ynab/ing_ynab:latest`

We mount the `state` file to prevent duplicates.

## Configuration

The configuration is done via environment variables:

* `START_DATE`: The date to start getting transactions.

### YNAB

* `YNAB_ACCESS_TOKEN`: Go to your budget settings to create one.
* `YNAB_BUDGET_ID`: On the webpage of your budget the last number in the path.
* `YNAB_ACCOUNT_ID`: On the webpage of the account the last uuid in the path.

### FinTS

* `FINTS_LOGIN`: The login id of your ING account (the last ten digits of your IBAN).
* `FINTS_IBAN`: The IBAN of the account you want to add.
* `FINTS_PIN`: The ping (password) of your ING account (leave empty to be prompted).
* `FINTS_PRODUCT_ID`: Your FinTS product ID (leave empty to use the python-fints one, though that's discouraged).

## FAQ

### Why did you violate Python convention X?

This is my first python project, feel free to open an issue or even a PR!

### Why are there no tests?

There are a few things that are really hard to test without real credentials. 
The rest should be tested (and will be in the future).
