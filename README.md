# Cribl Pack for ClamAV
----

Use this pack to reformat and enhance your ClamAV logs.

### For clamav.log
* ROUTE: Looks for string `-- SCAN SUMMARY --`
    * Should be very reliable
* Parse the parameters into JSON
* Put found files into a `_raw.found[]` array
* Set index time field `infected` to the number of found files if any
* Set _time to the Start time, remove `Start time` and `End time`, and clean up `Time` (duration)
* Check and fix _time if it's in the wrong timezone
* Set index, host, source and sourcetype if not present
* RESULT: Reliable _time; pure JSON event is easier to search; roughly 50% volume reduction in _raw and 25% overall

### For clamd.log
* ROUTE: Looks for string `clamd` in either source or sourcetype
    * May need adjustment
* Optional drop of status OK messages (disable Rule 1 if you want these)
* Trim redundant time(s) (we already have time extracted)
* Set index, host, source and sourcetype if not present
* Check and fix _time if it's in the wrong timezone
* RESULT: Reliable _time; shorter messages; roughly 80% drop in log volume (from sample data)

### For freshclam.log
* ROUTE: Looks for string `fresh` in either source or sourcetype
    * May need adjustment
* Drop hyphen only events
* Trim redundant time(s) (we already have time extracted)
* Set index, host, source and sourcetype if not present
* Check and fix _time if it's in the wrong timezone
* RESULT: Reliable _time; shorter messages; less dupe data; less unusable data; roughly 40% drop in log volume


## Using the Pack

* Add the pack to your Cribl LogStream leader (or single node) instance
* Review the rules
* Upload some of your own sample data to make sure the result meets your requirements
* Point your source to the Pack either via Routes, the source definition `Result Routing` option, or Quick Connect
* The Routing rules internal to the Pack may need to be adjusted to identify the 3 types of logs
   * See ROUTE notes above to understand how it comes set-up by default


## Release Notes

### Version 1.0.0 - 2021-12-02
No changes, just made the release official

### Version 0.50 - 2021-11-25
Initial

## Contributing to the Pack
---
Discuss this pack on our Community Slack channel #packs

## Contact
---
The author of this pack is Jon Rust <jrust@cribl.io>.

## License
---
This Pack uses the following license: [`Apache 2.0`](https://github.com/criblio/appscope/blob/master/LICENSE).


