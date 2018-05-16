<<<<<<< HEAD
# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
=======
# testapp
>>>>>>> 979a7288fc7ce1ecef6a545570b9bb5c112f8564

notes
https://web.archive.org/web/20160531044930/http://blog.crowdint.com/2014/02/18/fancy-calendars-for-your-web-application-with-fullcalendar.html

1. Gemfile
-gem 'fullcalendar-rails'
-gem 'momentjs-rails'
-bundle install

2. application.css
*= require fullcalendar

3. application.js
//= require moment 
//= require fullcalendar

$(document).ready(function() {

    // page is now ready, initialize the calendar...

    $('#calendar').fullCalendar({
        events: '/events.json' <---this line is to to insert events into calendar, remove if not needed
    });

});

4. application.html.erb
insert above all javascript
<script src="http://code.jquery.com/jquery-1.11.3.min.js"></script>

5. ...html.erb (to display calendar)
<div id="calendar"></div>

6. app/views/(folder name)/(page name).json.builder
-replace below according to table & column name
json.array!(@events) do |event|
  json.extract! event, :id, :title, :description
  json.start event.start_time
  json.end event.end_time
  json.url event_url(event, format: :html)
end

7. ...html.erb (to display calendar)
-these codes above calendar to add, edit, delete event (change path names accordingly)
<h1>Events</h1>

<table>
  <thead>
    <tr>
      <th>Title</th>
      <th>Description</th>
      <th>Start time</th>
      <th>End time</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <% @events.each do |event| %>
      <tr>
        <td><%= event.title %></td>
        <td><%= event.description %></td>
        <td><%= event.start_time %></td>
        <td><%= event.end_time %></td>
        <td><%= link_to 'Show', event %></td>
        <td><%= link_to 'Edit', edit_event_path(event) %></td>
        <td><%= link_to 'Destroy', event, method: :delete, data: { confirm: 'Are you sure?' } %></td>
      </tr>
    <% end %>
  </tbody>
</table>

<br>

<%= link_to 'New Event', new_event_path %>