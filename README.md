# Election_Analasys

## Project Overview
A Colorado Board of Elections employee has given you the following tasks to complete the election audit of a recent local
congressional election.

1.  Calculate the total number of votes cast.
2.  Get a complete list of candidates who received votes.
3.  Calculate the total number of botes each candidate received.
4.  Calculate the percentage of votes each candidate won.
5.  Determine the winner of the election based on the popular vote.

## Resources
- Data Source:  election_results.csv
- Software:  Python 3.9.2, Visual Studio Code, 1.61.0

## Summary
The analysis of the election show that:
- There were 369,711 votes cast in the election.
- The candidates were:
  - Charles Casper Stockham
  - Diana DeGette
  - Raymon Anthony Doane
- The candidate results were:
  - Charles Casper Stockham received 23.0% of the vote and 85,213 number of votes
  - Diana DeGette received 73.8% of the vote and 272,892 number of votes
  - Raymon Anthony Doane received 3.1% of the vote and 11,606 number of votes
- The winner of the election was:
  - Diana DeGette, who received 73.8% of the vote and 272,892 number of votes

## County Summary
The county analysis of the election show that:
- There were 369,711 votes cast in the election.
- The counties were:
  - Jefferson
  - Denver
  - Arapahoe
- The county turnout results were:
  - In Jefferson County 10.5% of the votes were cast totaling 38,855 number of votes
  - In Denver County 82.8% of the votes were cast totaling 306,055 number of votes
  - In Arapahoe County 6.7% of the votes were cast totaling 24,801 number of votes
- The county with the largest turnout in the election was:
  - Denver County which 82.8% of the votes were cast totaling 306,055 number of votes

## Election-Audit Summary
Using this script we were able to count 369,711 and determine the above results in a matter
of seconds from a CSV file.  This script determines the number of candidates and the number
of counties and therefore could be expanded all the way to state-wide elections with an un-
limited number of candidates.  With minor additions to the script, since the processes would
not change for the most part, other relevant districts could be added such as precints and
legislative districts.  In the code below, we only need to change "DISTRICT" to the relevant
district (i.e. precinct or legislative district [LD]).

    # 6a: Write a for loop to get the county from the county dictionary.
    for DISTRICT_name in DISTRICT_votes.keys():
        # 6b: Retrieve the county vote count.
        DISTRICT_vote_count = DISTRICT_votes.get(DISTRICT_name)
        # 6c: Calculate the percentage of votes for the county.
        DISTRICT_percentage = float(DISTRICT_vote_count) / float(total_votes) * 100
        DISTRICT_results = (
            f"{DISTRICT_name}:  {DISTRICT_percentage:.1f}% ({DISTRICT_vote_count:,})\n")

         # 6d: Print the county results to the terminal.
        print(DISTRICT_results)
         # 6e: Save the county votes to a text file.
        txt_file.write(DISTRICT_results)
         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (DISTRICT_name > DISTRICT_largest_count) and (DISTRICT_percentage > DISTRICT_largest_percentage):
            DISTRICT_largest_count = DISTRICT_vote_count
            largest_DISTRICT_name = DISTRICT_name
            DISTRICT_largest_percentage = DISTRICT_percentage

This script can only handle one race at a time but could be modified with more adjustments than the 
districts, to count up multiple races at the same time so that all races could be placed in a single 
CSV file and all results calculated concurrently.  You would need to adding a column indicating the 
race and adding a tally for "race" using a similar structure to candidate names or county names such as
below:

     for row in reader:
          # Add to the total vote count
          total_votes = total_votes + 1

          # Get the race name from each row.
          race_name = row[2]

          # 3: Extract the race name from each row.
          race_name = row[1]

          # If the race does not match any existing race add it to
          # the race list
          if race_name not in race_options:

              # Add the race name to the race list.
              race_options.append(race_name)

              # And begin tracking that candidate's voter count.
              race_votes[race_name] = 0

Additional scripting would also need to be developed to segregate the individual elections from each other.
It goes without saying that the more data added would slow the processing time down but would still be sig-
nificantly faster than hand tallying.
