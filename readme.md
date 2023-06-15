# Python

## Running with GitHub Actions

To run your Python script using GitHub Actions, follow these steps:

- Create an `actions.yml` file in the `.github/workflows` folder of your repository.
- Add the following script to `actions.yml`:

```bash
name: run main.py # Add your filename.py

on:
schedule: # Add time corresponding to UST time
    # - cron: '*/5 * * * *' # At every 5 minute
    # - cron: '0 8 * * *' # At every 8:00 AM
    - cron: '29 2 * * *' # At Utc 02:29 AM is indian time  of 7:59 AM

jobs:
    build:
        runs-on: ubuntu-latest
        steps:

        - name: checkout repo content
            uses: actions/checkout@v2 # checkout the repository content to github runner

        - name: setup python
            uses: actions/setup-python@v4
            with:
            python-version: '3.9' # install the python version needed
            
        - name: install python packages
            run: |
            python -m pip install --upgrade pip # upgrading pip version
            # Add your python dependencies
            pip install pandas
            
        - name: execute py script # for running main.py
            env:
            SENDER_EMAIL: ${{ secrets.SENDER_EMAIL }}
            PASSWORD: ${{ secrets.PASSWORD }}

            run: python main.py # Add your filename.py
```