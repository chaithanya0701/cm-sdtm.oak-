# cm-sdtm.oak-
reference code for intervention domain 

#reading the dm dataset
dm <- read.csv(system.file("raw_data/dm.csv",
                           package = "sdtm.oak"
))

study_ct <- read.csv(system.file("raw_data/sdtm_ct.csv",
                                 package = "sdtm.oak"
))

##The oak_id_vars is a crucial link between the raw datasets and the mapped SDTM domain

cm_raw <-
  generate_oak_id_vars(
    raw_dat = cm_raw,
    pat_var = "PATNUM", #patient id in raw dataset
    raw_src = "cm_raw"
  )
cm <-
  # Map topic variable
  assign_no_ct(
    raw_dat = cm_raw,
    raw_var = "MDRAW",
    tgt_var = "CMTRT"
  ) %>%
  # Map CMGRPID
  assign_no_ct(
    raw_dat = cm_raw,
    raw_var = "MDNUM",
    tgt_var = "CMGRPID",
    id_vars = oak_id_vars()
  ) %>%
  # Map qualifier CMDOSU
  assign_ct(
    raw_dat = cm_raw,
    raw_var = "DOSU",
    tgt_var = "CMDOSU",
    ct_spec = study_ct,
    ct_clst = "C71620",
    id_vars = oak_id_vars()
  ) %>%
  # Map CMSTDTC. This function calls create_iso8601
  assign_datetime(
    raw_dat = cm_raw,
    raw_var = c("MDBDR", "MDBTM"),
    tgt_var = "CMSTDTC",
    raw_fmt = c(list(c("d-m-y", "dd mmm yyyy")), "H:M"),
    raw_unk = c("UN", "UNK"),
    id_vars = oak_id_vars(),
    .warn = TRUE
  )
# problems(cm$CMSTDTC) to check if there are any parsing problems on a created variable
