# Space-Efficient Representation of Entity-centric Query Language Models

This repository hosts the data released as part of the Interspeech 2022 publication titled "*Space-Efficient Representation of Entity-centric Query Language Models*" by Van Gysel et al. The data consists of a two-level grammar of weighted templates with entity slots, and a weighted list of entities that fill that slot.

The [templates](data/templates.csv.gz) represent use-case queries where a user instructs a virtual assistant to navigate, or interact with, a catalog of audible content (e.g., songs, artists, playlists, podcasts, etc.) with a weight that represents use-case importance. The [entities](data/entities.csv.gz) are a list of media entities extracted from a large-scale media catalog around December 2021 with a weight that represents the entity's popularity according to a popular online streaming service.

## Getting started

The templates and entities are stored as CSV files, compressed using GZIP. The following Python snippet allows you to parse the data:

	import gzip
	import csv
	import os
	
	data_dir = os.path.join(os.path.realpath(os.path.dirname(__file__)), 'data')
	assert os.path.isdir(data_dir)
	
	templates_path = os.path.join(data_dir, 'templates.csv.gz')
	assert os.path.isfile(templates_path)
	
	entities_path = os.path.join(data_dir, 'entities.csv.gz')
	assert os.path.isfile(entities_path)
	
	
	def load_entries(path):
	    with gzip.open(path, 'rt') as f:
	        reader = csv.DictReader(f)
	
	        yield from reader
	
	
	# Print the first 10 templates.
	print('Top-10 templates:')
	for _, entry in zip(range(10), load_entries(templates_path)):
	    print(entry)
	
	print()
	
	# Print the first 10 entities.
	print('Top-10 entities:')
	for _, entry in zip(range(10), load_entries(entities_path)):
	    print(entry)
	
	print()

When executed, this prints the following output:

	Top-10 templates:
	{'unnormalized_prior': '57637551.0', 'text': 'hey Siri play <ENTITY>'}
	{'unnormalized_prior': '39276474.0', 'text': 'play <ENTITY>'}
	{'unnormalized_prior': '3447328.0', 'text': 'Siri play <ENTITY>'}
	{'unnormalized_prior': '1938007.0', 'text': 'hey Siri play the song <ENTITY>'}
	{'unnormalized_prior': '1880284.0', 'text': 'hey Siri <ENTITY>'}
	{'unnormalized_prior': '1866158.0', 'text': '<ENTITY>'}
	{'unnormalized_prior': '1446139.0', 'text': 'play the song <ENTITY>'}
	{'unnormalized_prior': '1413427.0', 'text': 'hey Siri play <ENTITY> music'}
	{'unnormalized_prior': '1265844.0', 'text': 'hey Siri who sings <ENTITY>'}
	{'unnormalized_prior': '998550.0', 'text': 'hey Siri play some <ENTITY>'}
	
	Top-10 entities:
	{'unnormalized_prior': '667.5385373950351', 'text': 'hip hop rap'}
	{'unnormalized_prior': '489.17729342016963', 'text': 'Pop'}
	{'unnormalized_prior': '379.43119497564226', 'text': 'R&B'}
	{'unnormalized_prior': '362.88422257786624', 'text': 'alternative'}
	{'unnormalized_prior': '334.26272050577774', 'text': 'rock'}
	{'unnormalized_prior': '326.4236190113619', 'text': 'country'}
	{'unnormalized_prior': '234.22980267171658', 'text': 'Holiday music'}
	{'unnormalized_prior': '214.52684952882836', 'text': 'soundtracks'}
	{'unnormalized_prior': '194.4645101369402', 'text': 'hard rock'}
	{'unnormalized_prior': '180.5184652443179', 'text': 'dance'}

## Citation

If you use the data hosted in this repository within your scientific publication, please refer to our [Interspeech 2022](https://machinelearning.apple.com/research/space-efficient-representation) paper:

```
@inproceedings{VanGysel2022phirtn,
  title={Space-Efficient Representation of Entity-centric Query Language Models},
  author={Van Gysel, Christophe and Hannemann, Mirko and Pusateri, Ernie and Oualil, Youssef and Oparin, Ilya},
  booktitle={Interspeech},
  year={2022},
}
```

## License

The content of this repository is licensed under the [Apple Sample Code License](LICENSE).