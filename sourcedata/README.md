# sourcedata/BRIS — reconstructed BrainVision headers for 4 control recordings

The University of Bristol (BRIS) `control` recordings for **bris04, bris09, bris17, bris36**
are shipped here in raw BrainVision format (`.eeg` + `.vmrk` + `.vhdr`), 32-channel, 1000 Hz.

The upstream source (OSF `eyzaq`, Nieuwland et al. 2018) provides these four recordings' `.eeg`
and `.vmrk` but their `.vhdr` headers are **truncated (1250 bytes) or missing**, which makes the
recordings unreadable. The `.vhdr` here were **reconstructed** from a sibling BRIS control header
(`bris01_control.vhdr`): the channel table and acquisition parameters are uniform across all BRIS
control recordings, so only the `DataFile`/`MarkerFile` pointers differ. Each reconstructed header
was verified to read correctly with `mne.io.read_raw_brainvision` (32 ch, 1000 Hz, ~735 markers;
e.g. bris09 = 643,780 samples).
