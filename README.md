# Compensate Challenge

## Background - Carbon emission-reduction projects

Compensation payments go in full to projects removing carbon from the atmosphere. Purchases are guided by Compensate’s independent Scientific Advisory Panel and certified with Gold Standard and Verified Carbon Standard, with the highest levels of transparency and verification.

In general, the term "emission-reduction project" refers both to projects that reduce greenhouse-gas emissions and projects that remove carbon dioxide from the atmosphere. For the sake of clarity, we divide such projects into two categories. In our terminology, a carbon-emission reduction project is one that reduces emissions (for example, a wind-power project). Meanwhile, a carbon-capture project is one that removes carbon dioxide from the atmosphere (for example, an afforestation project).

One emission-reduction unit is equivalent to the removal of one tonne of carbon dioxide (1,000 kg CO2) from the atmosphere. Compensate purchases emission-reduction units from carbon-capture projects. The price of the units is determined by the market and by the particular characteristics of different projects.

There are a number of different types of projects: forest protection, reforestation, CO2-removal and so on.

We primarily purchase emissions reduction units from projects that focus on forests, but we are constantly in search for the most sustainable and efficient ways to remove carbon dioxide from the atmosphere. Compensate invests in the planting of new forests and the protection of existing forests. We will always be open and transparent in our operations and make information on the use of compensation payments publicly available on our website.

The amount of carbon captured by each tree species is measured based on different characteristics, such as height and thickness of the tree and the hardness of the wood. For example, the harder the wood, the higher the carbon content of a tree. These carbon-capture calculations are determined individually for each species of tree by independent, third-party verification experts. In turn, these calculations are then used by the operators of carbon-capture projects.

## The task

Your challenge is to create an application that can be used to help optimize how Compensate purchases credits. Note: This example is simplified. Compensate has an independent scientific advisory panel to make the purchasing decisions.

Application must be a command line application which takes a path to a JSON file as a command line argument.

This JSON file will contain a JSON array of available projects. Project object contains information like project ID, group, project type, co2_volume, price of emission-reduction unit, min and max credits available to be bought from this project, time and continent.

One important thing is the time field. It describes how long it takes to capture all the CO2 from the atmosphere. Time unit is `day`, `month` or `year`. For example reforestation is cheap, but growth of the trees can take more than a hundred years. You can assume that the carbon removal process is linear, so that if reforestation takes one hundred years to complete, after fifty years it has been captured 0.5 of target value.

The Continental code tells roughly about where the project is located. Continent information is important since you should distribute the risk of success. Different continents provide different setup of projects. Continent code definition:

| Code | Continent Description |
| --- | --- |
| c1 | Africa |
| c2 | Asia |
| c3 | Europe |
| c4 | North America |
| c5 | South America |
| c6 | Antarctica |
| c7 | Australia |

An example of the input JSON file:

```
input.json

[{
    "id": "p1",
    "group": "short_term",
    "type": "capture",
    "co2_volume": 1.0,
    "price": 232.0,
    "min_credits": 5,
    "max_credits": 200,
    "time": 2,
    "time_unit": "day",
    "continent": "c1",
  },
  {
    "id": "p2",
    "group": "medium_term",
    "type": "protection",
    "co2_volume": 30,
    "price": 100.0,
    "min_credits": 5,
    "max_credits": 400,
    "time": 10,
    "time_unit": "year",
    "continent": "c1"
  },
  {
    "id": "p3",
    "group": "long_term",
    "type": "reforestation",
    "co2_volume": 30,
    "price": "10",
    "min_credits": 5,
    "max_credits": 500,
    "time": 140
    "time_unit": "year",
    "continent": "c2"
  },
  ...
]
```

Download a full example JSON here. [COMING SOON!]

Your application should calculate solution for purchase plan as follows:
- Minimize the risk by distributing projects over different continents as requested
- Minimize the risk by distributing projects over different kind of groups (short, medium, long) as requested
- Calculate the optimal volume of CO2 removed from atmosphere using provided target years and given budget
- Calculate report what is the amount of CO2 removed yearly from current year to target year using this optimal plan
- Provide solution as a list of projects and the number of credits to be bought
- Export the result to JSON file

Application should take following parameters to control how calculation should be done:

```
$ myapp [-file <path>]                      Source file of projects
        [-target <path>]                    Target file where result is stored
        [-money=<value>]                    Amount of money to be used, defaults to 0
        [-target_years=<value>]             Target years for C02 optimization, defaults to 1
        [-min_continents=<value>]           Minimum number of continents where projects should be distributed, defaults to 1
        [-min_short_term_percent=<value>]   Minimum percentage of short term projects to be bought, defaults to 0
        [-min_medium_term_percent=<value>]  Minimum percentage of medium term projects to be bought, defaults to 0
        [-min_long_term_percent=<value>]    Minimum percentage of long term projects to be bought, defaults to 0
```

For example, if have 1000 unit of money and you would like to optimize the plan for 30 years, distribute the risk to four continents, and make sure that the purchase plan contains at least 10% percentage of medium term and 30% percentage of long term carbon removal:

```
$ myapp -file input.json -target output.json -money=1000 -target_years=30 -min_continents=4 -min_medium_term_percent=10 -min_long_term_percent=30
```

Exported JSON file should contain the list of optimal selected projects and amount of credits to be bought. There should also be the solution of C02 removed as cumulative yearly report.
Following example describes the format of this JSON file (this is not a correct answer for the example input.json):

```
export.json

{
  "purchase_plan": [
    {
      "project_id": "p1",
      "num_credits": 1,
      "price": 232.0
    },
    {
      "project_id": "p2",
      "num_credits": 2,
      "price": 200.0
    },
    {
      "project_id-id": "p3",
      "num_credits": 56,
      "price": 560.0
    }
  ],
  "co2_report": [
    {
      "year": 2019,
      "co2_removed": 1.1
    },
    {
      "year": 2020,
      "co2_removed": 3.2
    },
    {
      "year": 2021,
      "co2_removed": 6.5
    },
    ...
    {
      "year": 2049,
      "co2_removed": 252.3
    }
  ]
}
```

You can choose the programming language freely as long as it can be executed from the command line.

You must provide the source codes for the written application and it must be compilable (if applicable) with a single command. You must provide necessary instructions on how to do the compilation.

Grading of the assignment is based on the following criteria:

Code structure and elegance
Correctness of the execution
Performance

Document and share your solution and code with us using Github, email, FAX. Style is free.

If you have any questions about the challenge or technical details, please contact Compensate Team:

Tobias Rask tobias.rask@fourkind.com

Good Luck! We will be more than happy to talk about your solution.
