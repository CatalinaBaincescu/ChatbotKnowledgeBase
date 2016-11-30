

<b>Chatbot Knowledge Base</b>

Team members: Baincescu Catalina, Birsan Alexandra, Gusa Diana, Iacob Madalina, Astefanesei Iulian

	1. Define a schema (question and answer)
	2. Define a schema for synonyms
	3. Define the endpoints for dictionary
	4. Define the endpoints for question and answer
	

Collection Q&A
	
	{
		"title": " Question and answer",
		"type": "object",
		"properties": {
			"question": {
				"type": "string"
			},
			"answer": {
				"type": "string"
			}
		}
	}

Example: 

	{
		"question": "How is Albert Einstein?",
		"answer": "Albert Einstein was a German-born physicist who developed the general theory of relativity, among other feats. He is considered the most influential physicist of the 20th century."
	}


Collection Word

	{
		"title": " Word",
		"type": "object",
		"properties": {
			"word": {
				"type": "string"
			},
			"partOfSpeech": {
				"type": "string",
				 "oneOf" : [
					"noun", "pronoun", "verb", "adjective", "adverb", "preposition", "conjunction", "interjection"
				]
			},
			"definitions": {
				"type": "array",
				"items": {
					"title": "a definition",
					"type": "string"
				}
			},
			"wordSynonyms": {
				"type": "array",
				"items": {
					"title": "a synonyms",
					"type": "string"
				}
			}
		}
	}
Example: 

	{
		"word": "apple",
		"partOfSpeech": "noun",
		"definitions": [
			"The round fruit of a tree of the rose family, which typically has thin green or red skin and crisp flesh.",
			"Used in names of unrelated fruits or other plant growths that resemble apples in some way, e.g. custard apple, oak apple."
		]
		"properNoun": "apple"
	}

GET  /api/dictionary?word=apple&partOfSpeech=noun
	
	{
		"isValidWord": true,
		"wordDefinition": [
			"The round fruit of a tree of the rose family, which typically has thin green or red skin and crisp flesh.",
			"Used in names of unrelated fruits or other plant growths that resemble apples in some way, e.g. custard apple, oak apple."
		],
		"error": false
	}

GET  /api/dictionary?word=llllll&partOfSpeech=preposition

	{
		"isValidWord": false,
		"wordDefinition": null,
		"error": true,
		"errorMessage": "word not found",
		"errorId": "404"
	}

GET  /api/synonyms?word=model&partOfSpeech=noun

	{
		"wordSynonyms": ["miniature", "standard"],
		"error": false
	}

GET  /api/properNoun?word=model

	{
		"shortDefinition": "A system or thing used as an example to follow or imitate.",
		"definitionSource": "https://en.oxforddictionaries.com/definition/model",
		"error": false
	}




