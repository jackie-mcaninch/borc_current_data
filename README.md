# Servo Current/Event Analysis

This experiment was conducted by installing a calibrated BORC onto our simulation workbench, which consists of a radiator valve attached to an air compressor to enable a controllable amount of air flow. The BORC was instructed to move from its `servo_min` to `servo_max` (or vice versa depending on the direction of the test) in 20 iterations. At each step, a time series of current readings from the BORC's servo was recorded internally by the BORC logging function. The point of this experiment is to map the differences in current to physical events that happened on the workbench, and our focus is on these two events:

- Actuator comes into or out of contact with the valve plunger
- Air flow through the valve is started or halted

In-depth record of qualitative, physical observations can be found in [this spreadsheet](https://docs.google.com/spreadsheets/d/17k65DrAm_Nwnbxt5K5YbKa-UJvGwfOEQxszsrH3pXGQ/edit#gid=0). A summary of these observations is provided in [`observations.csv`](#observation-data).

## Trial results
Time series current results from each trial are stored in files following the format `TX_direction_Y_Ypsi.csv`, where `X` is the trial number and `Y` is the PSI of the air flow from the compressor. The `direction` is labeled as *forward* if we traverse from valve-open to valve-closed, and *backward* if we traverse from valve-closed to valve-open. **TEMPORARILY IGNORE FILE HEADER, COLUMN NAMES ARE INACCURATE.** Each record has 4 columns as follows:

- `time`: timestamp, expressed in milliseconds since the start of the experiment.
- `measurement`: the attribute we are measuring - this column can be ignored.
- `mA`: the value of the current read from the servo at the present time, in milliamps.
- `iter`: the step from 0 to 19 at which we recorded the row data.

## Observation data
As mentioned previously, we are interested only in the events regarding a change in state for (a) contact between the BORC's actuator and the valve plunger, and (b) the presence of air flowing through the valve. Changes in states always occur in between iterations, so columns denote the iteration number which happened before and after the event occurred. For example, if the trial was a backward test and we heard the initial air hissing sound in between iterations 4 and 5, we record 4 and 5 for the before and after air flow columns, respectively. On a forward test, we would record the point at which the air flow stopped instead of started. There is one row for every trial (corresponding to its data file above), each of which contains 6 columns as follows:

- `trial`: ID of the trial which corresponds to the data file names.
- `is_backward_test`: 1 if traversing from valve-closed to valve-open, otherwise 0.
- `before_contact_event`: The iteration number which occurred before a change in contact state was observed.
- `after_contact_event`: The iteration number which occurred after a change in contact state was observed.
- `before_sealed_event`: The iteration number which occurred before a change in air flow state was observed.
- `after_sealed_event`: The iteration number which occurred after a change in air flow state was observed.