# coffeetalk
Random coffee meetup generator

![coffee talk](https://media.giphy.com/media/3oz8xIuzYcJLlrVFII/giphy.gif)

I saw the https://randomcoffee.me/ article but am unable to get access to the Beta, so I think it'd be fun to try and make my own, using README driven development to think out the problem first.

## How this could work

My initial idea is to have Friday (coffee feedback day), broken up into 30min chunks all-day. Users will select times that are good for them earlier in the week and the day before the system will random assign you to another person in that time slot. 

## Google Calendar Appoinment Slots

This would be the easiest interface because employees would have access to this calendar and it allows them to block off that time.

~[Google Calendar appointment slots](https://www.ditoweb.com/wp-content/uploads/2016/01/appointment-pop-up-1024x737.png)

## Steps

1. User selects 30min chunks in Google Calendar that they are free
2. On Thursday the system randomly assigns coffee-buddy from calendar invites
3. Email is sent out, or calendar is updated with match-ups
3. Users meet up and grab that coffee (tea, juice)

# Technology

- Node
- AWS Lambda with Scheduled Events
- DynamoDB to store matchups and users

A Node lambda would be the best use case for me, due to the existence of a prebuilt Google API SDK and ability to run on demand. Using [scheduled events](https://docs.aws.amazon.com/lambda/latest/dg/with-scheduled-events.html), it can grab all of the calendar events at a certain time on Thursdays and process the randomization. Since we are in AWS land, we can also store all the matchups and member info in Dynamo.

An alternative would be to use Google's Cloud Functions, but I will opt for AWS to eventually migrate it over to our system. Google also doesn't seem to give any preference to GCF when contact their own servers (authenticated SDKs and what not).

## Backlog of Concerns and Ideas

- [ ] Randomization must take into account minimizing repeat meetups 
- [ ] System must allow for cancellation and notification
- [ ] Odd numbers of calendar participants
- [ ] Need follow up information on performance of system
- [ ] It could divy up users to Ground Support / Jack's to reduce lines
- [ ] Prioritize those who missed a match-up previously (randomly or through cancellation)
- [ ] Can calendar invite be updated with match ups and assigned coffee place?
