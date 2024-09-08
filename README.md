# Football Analysis Project no number 10s

This project analyzes the evolution of the traditional number 10 role in football, focusing on legendary players like Diego Maradona, Johan Cruyff, Kaká, Kevin De Bruyne, and James Rodríguez. The code in this repository uses various football datasets and visualization tools to generate heat maps and pass networks for matches played by these players, helping to visualize their positional play and tactical evolution.

## Libraries

The following Python libraries are used in this project:

- **[mplsoccer](https://mplsoccer.readthedocs.io/en/latest/)**: Used for generating heat maps and pass networks for players.
- **[statsbombpy](https://github.com/statsbomb/statsbombpy)**: Allows access to StatsBomb's open-data football datasets.
- **pandas**: For data manipulation.
- **seaborn**: For additional visualization support.
- **matplotlib**: To plot graphs and images.

You can install the required libraries by running:
```bash
!pip install mplsoccer statsbombpy pandas seaborn matplotlib
```

## Datasets

The analysis pulls football match data from several competitions including:

- FIFA World Cup (1986, 1990)
- Champions League (Ajax in the 1970s, AC Milan in 2006-07)
- Copa America (Colombia)
- Euro (Belgium)

## Usage

1. **Competitions & Matches**
   - Retrieve data for various competitions and filter specific matches based on teams and competitions.
   - Example: Retrieving all Colombia matches in Copa America 2024 or Argentina’s matches in FIFA World Cups 1986 and 1990.

   ```python
   CA24 = sb.matches(competition_id=223, season_id=282)
   col_matches = CA24[(CA24['home_team'] == 'Colombia') | (CA24['away_team'] == 'Colombia')]
   ```

2. **Heat Maps**
   - Heat maps show the positional activity of players during specific matches.
   - Example: Creating a heat map for Johan Cruyff during an Ajax match:

   ```python
   pitch = Pitch(pitch_type='statsbomb', line_zorder=2, pitch_color='black', line_color='white')
   fig, ax = pitch.draw(figsize=(13.8, 8.5))
   ax.set_title('Johan Cruyff Heat Map', fontsize=14, color='black')
   pitch.kdeplot(ajax_cruyff['x'], ajax_cruyff['y'], shade=True, cmap='gnuplot', ax=ax)
   plt.savefig('Johan_Cruyff_Heat_Map.png')
   plt.show()
   ```

   Heat maps are generated for each player in different matches, showcasing where they spent most of their time on the pitch.

3. **Pass Networks**
   - Pass networks depict the distribution of passes between players and their positioning on the field.
   - Example: Building a pass network for Johan Cruyff in a specific Ajax match:

   ```python
   pass_line = pitch.lines(pass_between.x, pass_between.y, pass_between.x_end, pass_between.y_end, lw=pass_between['count'], color='white', zorder=1, ax=ax)
   nodes = pitch.scatter(avg_position['x'], avg_position['y'], s=20*avg_position.pass_count, color='red', edgecolors='black', linewidth=1, alpha=1, ax=ax)
   ```

   Each pass network visualizes how key players were involved in distributing the ball during matches.

4. **Player-Specific Analysis**
   - Analyze key players like Diego Maradona, Johan Cruyff, Kaká, Kevin De Bruyne, and James Rodríguez through their touch, positional, and pass data.
   - For example, Maradona’s positional heat maps from the 1986 and 1990 World Cups showcase his deeper involvement in certain matches:

   ```python
   arg_maradona = arg[arg['player_id'] == 38641]
   pitch.kdeplot(arg_maradona['x'], arg_maradona['y'], shade=True, cmap='plasma', ax=ax)
   plt.savefig('maradona.png')
   ```

## Structure

- **`Sports Analysis 10s.ipynb`**: Main notebook containing the code to generate heat maps and pass networks.
- **`images/`**: Directory containing generated heat maps and pass networks for each player.
- **`data/`**: Contains the datasets used for analysis (if needed).

## How to Run the Code

1. Install the required libraries using the command mentioned above.
2. Run the code in the `Sports Analysis 10s.ipynb` notebook. The data for matches and players will be fetched from StatsBomb’s open data.
3. Heat maps and pass networks will be generated for the players.
