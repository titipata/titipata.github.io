---
title: trick in sentence split
---

I just found a trick to tackle sentence split better on [Stack Overflow](http://stackoverflow.com/questions/42445842/how-to-split-text-into-sentences-when-there-is-no-space-after-full-stop)

The problem is you can have the text that can have `.` between sentences like `activities.President`.
Here is the full text example from SO:

```python
text = """
A gas well near Surabaya in East Java operated by Lapindo Brantas Inc. has spewed steaming mud since
May last year, submerging villages, industries and fields.A gas well near Surabaya in East Java operated
by PT Lapindo Brantas has spewed steaming mud since May last year, submerging villages, factories and fields.Last week,
Indonesia's coordinating minister for social welfare, Aburizal Bakrie, whose family firm controls Lapindo Brantas, said
the volcano was a "natural disaster" unrelated to the drilling activities.President Susilo Bambang Yudhoyono last month
ordered Lapindo to pay 3.8 trillion rupiah (420.7 million dollars) in compensation and costs
"""
```

In the answer, he wrote some regex to replace that with `. ` so that
sentence splitter works fine.

```python
text = re.sub(r'\.(?=[^ \W\d])', '. ', text)
sent_detector = nltk.data.load('tokenizers/punkt/english.pickle')
sent_detector.tokenize(text.strip())
```

I found it useful.
