---
layout: post
title:      "Structuring my React application"
date:       2017-12-02 00:06:36 +0000
permalink:  structuring_my_react_application
---


As I get closer to completing my React and Redux app, I thought I'd take the opportunity to write a blog about structure, since this has been one of the most challenging parts. My advice to other students is to plan out as much as possible in advance! The data model for this app initially seemed extremely simple compared to my Rails app, but, as I've been learning over the past week, there are still a lot of choices to make.

One of my big dilemmas was figuring out whether to connect to the Redux store directly with mapStateToProps/mapDispatchToProps or just pass the state or callback functions down as props. I initially started out connecting almost every component that needed to access state, but as I started to think about refactoring I changed some of these. I'd read some articles that talked about how great stateless functional components are. I'd also gone through a [series of video tutorials](https://www.youtube.com/watch?v=MhkGQAoc7bc&list=PLoYCgNOIyGABj2GQSlDRjgvXtqfDxKm5b) that suggested connecting to the store only when passing props started to seem awkward - a point I definitely hadn't reached.

But after doing more reading, it seems like having a single container component that passes down everything isn't necessarily the best way to do things, either. According to [one article I read](https://medium.com/dailyjs/quick-redux-tips-for-connecting-your-react-components-e08da72f5b3), it can be better to connect to the store directly in component because otherwise the entire page will re-render when state changes. So I ended up un-refactoring some of my refactors and tested both versions of the code with my navbar, which basically confirmed the information in the article: passing it props from the parent component results in rerendering with every state change, whereas connecting to the store directly does not. (Not that anyone would notice whether or not my miniscule navbar rerendered, but it's still nice to know I'm taking advantage of React's magic!)

Another structure-related hurdle I ran into was dealing with nested items in state. My project is an app to keep track of travel goals, so my state contains a list of trip objects. Users can also add activities that are associated with each trip. Based on my previous projects, it seemed obvious that activities should be nested under trips, both in the json sent from the server and in the Redux store. As it turns out, this was probably a mistake, since writing reducers for nested attributes can be a REAL pain. Especially if you want to delete one of the nested items. This is what the code to delete an activity ended up looking like, adapted from a [stackoverflow post](https://stackoverflow.com/questions/35342355/remove-data-from-nested-objects-without-mutating):

```
        case 'DELETE_ACTIVITY':
            function filterOut (state) {
                return (tripId, activityId) => {
                    return state.reduce((state, trip) => {
                        return state.concat(
                        (tripId === trip.id) ?
                            Object.assign({}, trip, {activities: trip.activities.filter((activity) => activity.id !== activityId)}) :
                            trip
                        );
                    }, []);
                }
            }
            return filterOut(state)(action.payload.tripId, action.payload.id)
```
