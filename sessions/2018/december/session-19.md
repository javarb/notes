# SOFTWARE ENGINEERING IN JAVA

## Session 19 (04/12/2018)

- Testing to HTTP endpoints
- Review past homeworks

### Notes:

#### Testing HTTP endpoints

We cloned the 'Talenhaven' Roger's repository and from it he was explaining to me all concepts related with reach HTTP endpoint from tests.

His approach was to buit a generic test to reach HTTP endpoints regardless the HTTP verb used.

#### Homework revision

Is recommended that the JS fronted shows results in text, this can be achieved using some library but the most simple thing to do is to return an JSON object in the API that contains a text with the calculated value and then use that string in the frontend.

**TIP:** Some popular frontend libraries that have all embeeded are React and Angular. As they have corresponding learning curves, [Create React App][1] can be useful.

by other side, about the `{}` being prefereable than `[]` at the beggining of a JSON file, besides of the security reason, another reason to prefeer `{}` is because if we need to change or add something to our response will be easier if we have an object instead an array. If we have an array, and want to return another thing, we'll have make a new object and add that new object to the JSON payload anyway.

###  Homework

- [ ] Deploy dependencies in docker-compose.yml in talenthaven-api


### Resources:
- [Create React APP - GitHub site][1]
- [Create React APP - GitHub repo][2]

[1]: https://facebook.github.io/create-react-app/
[2]: https://github.com/facebook/create-react-app
