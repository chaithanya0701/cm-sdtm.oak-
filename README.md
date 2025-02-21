
oak_id_vars()
syntax:-
generate_oak_id_vars(
raw_dat, 
pat_var, 
raw_src
)

Arguments
raw_dat	-The raw dataset (dataframe)
pat_var	-Variable that holds the patient number
raw_src	-Name of the raw source

assign_no_ct() 
maps a variable in a raw dataset to a target SDTM variable that has no
terminology restrictions.
syntax:- 
assign_no_ct(
  tgt_dat = NULL,
  tgt_var,
  raw_dat,
  raw_var,
  id_vars = oak_id_vars()
)

tgt_dat	
Target dataset: a data frame to be merged against raw_dat by the variables indicated in id_vars. This parameter is optional, see section Value for how the output changes depending on this argument value.

tgt_var	
The target SDTM variable: a single string indicating the name of variable to be derived.

raw_dat	
The raw dataset (dataframe); must include the variables passed in id_vars and raw_var.

raw_var	
The raw variable: a single string indicating the name of the raw variable in raw_dat.

id_vars	
Key variables to be used in the join between the raw dataset (raw_dat) and the target data set (raw_dat).

ct_spec	
Study controlled terminology specification: a dataframe with a minimal set of columns, see ct_spec_vars() for details.

ct_clst	
A codelist code indicating which subset of the controlled terminology to apply in the derivation.

Value
The returned data set depends on the value of tgt_dat:

If no target dataset is supplied, meaning that tgt_dat defaults to NULL, then the returned data set is raw_dat, selected for the variables indicated in id_vars, and a new extra column: the derived variable, as indicated in tgt_var.

If the target dataset is provided, then it is merged with the raw data set raw_dat by the variables indicated in id_vars, with a new column: the derived variable, as indicated in tgt_var.

assign_ct() 
maps a variable in a raw dataset to a target SDTM variable following controlled
terminology recoding.

syntax:-
assign_ct(
  tgt_dat = NULL,
  tgt_var,
  raw_dat,
  raw_var,
  ct_spec,
  ct_clst,
  id_vars = oak_id_vars()
  
assign_datetime() 
maps one or more variables with date/time components in a raw dataset to a
target SDTM variable following the ISO8601 format.

syntax:- 
assign_datetime(
  tgt_dat = NULL,
  tgt_var,
  raw_dat,
  raw_var,
  raw_fmt,
  raw_unk = c("UN", "UNK"),
  id_vars = oak_id_vars(),
  .warn = TRUE
)

Arguments
tgt_dat	
Target dataset: a data frame to be merged against raw_dat by the variables indicated in id_vars. This parameter is optional, see section Value for how the output changes depending on this argument value.

tgt_var	
The target SDTM variable: a single string indicating the name of variable to be derived.

raw_dat	
The raw dataset (dataframe); must include the variables passed in id_vars and raw_var.

raw_var	
The raw variable(s): a character vector indicating the name(s) of the raw variable(s) in raw_dat with date or time components to be parsed into a ISO8601 format variable in tgt_var.

raw_fmt	
A date/time parsing format. Either a character vector or a list of character vectors. If a character vector is passed then each element is taken as parsing format for each variable indicated in raw_var. If a list is provided, then each element must be a character vector of formats. The first vector of formats is used for parsing the first variable in raw_var, and so on.

raw_unk	
A character vector of string literals to be regarded as missing values during parsing.

id_vars	
Key variables to be used in the join between the raw dataset (raw_dat) and the target data set (tgt_dat).

.warn	
Whether to warn about parsing failures.
