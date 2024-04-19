# fitness-calculator
Calculator automating fitness estimation of microorganisms


This fitness calculator, designed for command-line use, processes CSV files with four columns: ID, lag_time, growth_rate, and max_OD. It normalizes each parameter to ensure comparability, assigns scores based on user-defined weights, and calculates a ‘fitness’ score by summing these scores. This holistic approach allows for comprehensive strain fitness comparison. The code also accounts for positive, negative, and medium controls to prevent artificial score skewing.

The code normalizes growth parameters for each strain and control, excluding zero lag time instances to avoid fitness score distortion. A new data frame is created with non-excluded values, and normalization parameters are reported. Fitness scores, dependent on assigned weights, are calculated by summing normalized parameters and reported in a ‘fitness_score’ column.

The choice of weight parameters should align with the specific biological phenomena under study, reflecting the biological relevance of each parameter. While normalization scores remain constant, fitness scores can vary significantly with changes in weight parameters, reflecting the biological phenomena being assessed. Different results with different weighted parameters are not inconsistencies, but reflections of how weights influence fitness score calculations.
