# Presenter

![mvp](../../mvp/mvp.png)

The Presenter is an object whose job is to take the Response Model and translate it into a View Model.

Response Model has data, created by an Interactor, as a result of an Use Case, but it is not presentable. For example, a date would be a Date Object. It is the job of a Presenter, to format the data into 'strings' or proper format for the View Model.

## Examples

* If we need to display negative currencies in red, the Presenter should let know the View Model to do so.
* If there's a button in the View Model that should be conditionally rendered, the Presenter should tell so to the View Model using a boolean.
* If there's not significant processing of the view data, then Presenter shouldn't be involved.

## Goal

The goal is to __make the View so stupid, that we don't have to test it__. We don't want to do any processing in the View Model.

You can test everything in the Presenter.

