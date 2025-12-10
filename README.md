# WellSpent

Publicly Hosted Website: https://well-spent.vercel.app/

Youtube Demo Link:

## Description:

The world problem that I chose for this project is water conservation. I
came to realize that water conservation is one of the least discussed
topics in my life and there is nothing that I found that quantifies the
amount of water we use. We always tell each other to conserve water and
to be mindful about using water, but I thought if I could quantify the
water we use and corelate to the impact it makes on our environment, we
would be more inclined to be careful and set limits. This is what led to
the creation of WellSpent.

WellSpent is a utility tracking app/website that is meant to track a
household\'s water usage. Ideas for this were taken from Duke Energy\'s
dashboard that I use for my electricity and gas usage. Based upon the
usage, I tend to alter the usage and be more considerate of the
appliances I\'m using.

WellSpent aims to capture the usage of water for a household and
breaking it down into specifics such individual tap usage, shower
lengths, water quality, trends in water usage, and an option to donate
to a non-profit organization determined to clean our water sources and
promoting sustainable water practices.

The main theme is to make sure that the numbers regarding water supply
are as visible as they can be and I believe WellSpent is the right step
towards that as it is something that can be applied to each household
(accessible) and will allow more people to be considerate of how much
water they use and if they go over, they have the match the amount they
went over their desired limit as a donation to water.org.

## Sketches:

### Sketch 1:

This sketch has a general idea of what I want to see in a dashboard
which would make sense for a consumer. Notice the dam feature--- that's
supposed to indicate how much water you have left out of the limit that
you chose. Obviously, this is not hardcoded to cut off your supply but
rather a way to encourage you to develop good habits.

!(assets/images/media/image1.png)

### Sketch 2:

Sketch 2 builds upon Sketch 1. It adds in the Setting Limit
functionality which allows for the user to set limits for each appliance
for how much water they should be using. Notice how the dam from the
previous sketch is now changed to represent a scenery of a lake. The
idea behind this is if you go over the limit you set, the environment
will turn into a desert helping you visualize the effects of your
overconsumption of water.

!(assets/images/media/image2.png)

### Sketch 3:

This Sketch builds upon the features we started to implement in Sketch
2. We add a tab about Learn More which ended up being a pay/donate tab
in the final prototype. The Remote-Control functionality shows how you
can turn on or off an appliance if you've forgotten helping you save
water. The history page helps us visualize the usage of water over the
last couple of months along with specific appliance-based usage which
helps you understand the breakdown of how you're using your water.

!(assets/images/media/image3.png)

### Sketch 4:

This was the final draft on which WellSpent ended up being based on. The
scenery as highlighted before is on the left side along with an expected
cost that we calculate based upon the limit we set for our appliances
and the actual cost for comparison. The middle column shows the list of
devices and the status it's in. The right column shows the water usage
in liters. The final prototype moves the Water Usage tab to the left
column and adds in a live flow activity graph and an appliance-specific
usage graph.

!(assets/images/media/image4.png)

## Final Prototype:

The final prototype consists of the main dashboard, view history, and
donate tabs. The main dashboard is split into 3 specific columns. I'll
go into detail below.

!(assets/images/media/image5.png)

For the Left Column, we have two possible scenarios for the scenery
screen. Depending on if you've exceeded the limit or not, the scenery
changes. If you're within the limit, it shows a green scenery showing
how you're helping conserve water and if you're shown a desert, it means
you're over the limit and need to be cautious of your water usage. The
expected cost and target costs are additionally calculated based on what
the limit you set for the month to be which can be edited using the
pencil icon.

!(assets/images/media/image6.png)
!(assets/images/media/image7.png)
!(assets/images/media/image8.png)

Moving onto the middle column- this section shows us the different
utilities that use water that we have. The top card shows the appliance
that is selected and its status.

!(assets/images/media/image9.png)

If we click Start, it's going to light up green, and the shower icon
will turn blue indicating that the utility is in use.

!(assets/images/media/image10.png)

A new utility can be added by using the "+Add Utility" button which
allows to add a new utility and classify it into the defined types so it
can be graphed. The limits set for the new utility are factored into the
calculation of the monthly limits and the donation amount.

!(assets/images/media/image11.png)

Now, let's move onto the right column, this consist of a live activity
graph which updates the flow of water over the last 30 seconds
constantly along with a static bar graph which is aimed to show the
utility-by-utility distribution of water consumption.

!(assets/images/media/image12.png)

The "View History" tab is a great way for us as users to ensure that we
can see how our water consumption has changed based upon new habits or
change in seasons. This page consists of the utility-distribution graph
from above along with monthly water consumption graph (static). Along
with the visuals, it also has the base to implement dynamic statements
for different utilities to show the exact usage and cost. This feature,
however is not implemented in the final prototype but the static data
shows how effective it can be.

!(assets/images/media/image13.png)

The donation page is something I'm quite proud of. It allows the user to
pay their water bill at the end of each month and have two scenarios.

### Scenario 1:

Your water usage was below the limit you set. You can pay the amount you
owe and have the option to make a donation towards water.org.

!(assets/images/media/image14.png)

### Scenario 2:

You have exceeded the limit for the month. You're going to have to pay
your water bill and are recommended a donation amount which is based
upon how much you've exceeded the limit in liters by and matching the
cost that you would pay for it essentially multiplying the exceeded
amount by 2. This allows for us to be more mindful when consuming water
and not wasting.

Yes, the link to water.org works!

!(assets/images/media/image15.png)

## Use of AI:

My use of AI in this assignment was mainly for the CSS for visual
components that I found hard to code such as the graph, scenery, and the
live flow chart. This along with continuous debugging on my end allowed
me to understand these concepts and not just plainly copy-paste them as
I knew what I wanted and was working towards a well-rounded
understanding of these concepts while also being able to debug what AI
helped me write.

## Future Work:

I was pleasantly surprised with how passionate I got about this project.
Initially, I was swaying between another habit tracker (sigh) and
de-phone your life app (also sigh). I'm glad I ended up choosing this
problem to fix with my UI.

I believe the potential to this UI is quite limitless but for the sake
of this assignment--- the main things that are left to implement is a
working view history section which generates statements along with the
graphs working, profile section which allows you to set-up your account
and add your friends to see who has the lowest water consumption and
also who doesn't shower if they have extremely low water consumption,
and finally, the ability to view where your water is being supplied from
along with the ability to view water outages and a Tips and Trick page
to help promote good water conservation habits.
