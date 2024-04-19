import subprocess
import sys

def install_pandas():
    try:
        import pandas as pd
        print("Pandas is already installed.")
    except ImportError:
        print("Pandas is not installed. Installing now...")
        subprocess.check_call([sys.executable, "-m", "pip", "install", "pandas"])
        print("Pandas has been installed.")

def install_numpy():
    try:
        import numpy as np
        print("Numpy is already installed.")
    except ImportError:
        print("Numpy is not installed. Installing now...")
        subprocess.check_call([sys.executable, "-m", "pip", "install", "numpy"])
        print("Numpy has been installed.")

# Call the function at the beginning of your script
install_pandas()
install_numpy()

import pandas as pd
import numpy as np

# Assuming df is your DataFrame and it has columns 'lag_time', 'growth_rate', 'max_OD'

while True:
	lag_time_weight = float(input("Enter the weight for lag_time (between 0.0 - 1.0): "))
	growth_rate_weight = float(input("Enter the weight for growth_rate (between 0.0 - 1.0): "))
	max_OD_weight = float(input("Enter the weight for max_OD (between 0.0 - 1.0): "))

	weights = {'lag_time': lag_time_weight, 'growth_rate': growth_rate_weight, 'max_OD': max_OD_weight}

	if sum(weights.values()) !=1:
		print("The weights do no sum up to 1. Please enter the weights again.")

	else:
		break

# Ask the user if they want to disregard any weights
disregard_weights = input("Do you want to disregard any weights? (yes/no): ")
if disregard_weights.lower() == 'yes':
    disregard = input("Which weight do you want to disregard? (lag_time/growth_rate/max_OD): ")
    weights[disregard] = 0

# Prompt the user for the file name
file_name = input("Enter the file name: ")

# Confirm before proceeding
proceed = input("Did you include a positive and/or negative control? (yes/no): ")
if proceed.lower() != 'yes':
    print("Please include a positive and/or negative control")
    exit()

weights = {'lag_time': lag_time_weight, 'growth_rate': growth_rate_weight, 'max_OD': max_OD_weight}

df = pd.read_csv(file_name)

parameters = ['lag_time', 'growth_rate', 'max_OD']

# Normalize the parameters
df_normalized = df.copy()
for parameter in parameters:
    if parameter == 'lag_time':
        # Create a separate DataFrame for lag_time where lag_time is not 0
        df_lag_time = df[df['lag_time'] != 0]
        min_val = df_lag_time[parameter].min()
        max_val = df_lag_time[parameter].max()
        # Normalize lag_time in the original DataFrame using min_val and max_val from df_lag_time
        df_normalized.loc[df_lag_time.index, parameter] = 1 - ((df_lag_time[parameter] - min_val) / (max_val - min_val))
    else:
        min_val = df_normalized[parameter].min()
        max_val = df_normalized[parameter].max()
        df_normalized[parameter] = (df_normalized[parameter] - min_val) / (max_val - min_val)

# Calculate the fitness score
df_normalized['fitness_score'] = np.dot(df_normalized[parameters], list(weights.values()))

print(f"Weights used: {weights}")
print(f"File name: {file_name}")

print(df_normalized)

# Ask the user if they want to export the results
export_results = input("Do you want to export the results? (yes/no): ")
if export_results.lower() == 'yes':
    # Ask the user for the export format
    export_format = input("Enter the export format (excel/csv): ")
    # Ask the user for the export file name
    file_name = input("Enter the export file name: ")
    if export_format.lower() == 'excel':
        df_normalized.to_excel(f'{file_name}.xlsx', index=False)
    elif export_format.lower() == 'csv':
        df_normalized.to_csv(f'{file_name}.csv', index=False)
    else:
        print("Invalid format. Please enter either 'excel' or 'csv'.")
else:
    print("Results will not be exported.")

input("Press enter to exit")
