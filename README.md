The code is implemented for the water consumption for civil uses in Tuscany provided by the Tuscany water authority (AIT).

The two databases are used as source data for the code:

- data_ut.csv - measurement database (meter readings)
- vol_ut.csv - database of users or water meters
The connection variable is the user identifier ( id_utente_ges).

In the measurements archive (ut_data) the fields to use are the following:

anno_consegna (reference year of the data being delivered)
id_gestore ( codes identified to date for Tuscan managers)
data_misura ( date of the measurement ATTEMPT)
valore_misura (measurement value)
id_utente_ges (user identification code)

The objective of the code development is to arrive at a database in which an average consumption volume is associated with each month/year for each water meter reading. To do this the following procedure is used:

1. Calculation  for each measurement (t) the period (number of months) that separates it from the previous one (t-1, obviously only starting from the second measurement in temporal order)

2. Calculation for each measurement the total consumption of the period that separates it from the previous one (also in this case starting from the second measurement in temporal order)

3. Calculation of average monthly consumption for all the months included in the period from t-1 to t;

4. Creation of observation for each month included in the period from t-1 to t for which the following is indicated: the average consumption calculated in step 3; the month of consumption; the year of consumption;  the handler code (id_gestore); the user identification code (id_utente_ges).

Once the monthly consumption database has been created for each water meter reading, the following variables contained in the user database are added to each of these records (using the id_user_ges variable as the linkage):

tipo_uso ( end user typology, 1 domestic resident)
x ("x" coordinates - point that originated the interruption)
y ( "y" coordinates - point that originated the interruption)
epsg (coordinate reference system)
id_rete (unique code of the network to which the meter refers)
note (Record annotations)
pro_com (code of province given by the concentration of the province code and the three-digit municipality code)
commune (name of municipality)

The code, then,  runs to perform the calculation of water consumption profiles (total values per month/year) classified by the municipality, by the handler type, and by type of user. Finally,  the code is used to plot histograms in R studio corresponding to the classifications of the water consumption profiles. 
