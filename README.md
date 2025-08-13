# news-to-telegram

A serverless script that scrapes news from designated websites and sends updates to a Telegram channel. This project is designed to monitor websites that do not offer RSS feeds or other notification mechanisms.

---

## The Problem

Many poorly-designed websites, such as local community pages, school portals, or blogs, do not provide RSS feeds. This makes it difficult to stay updated with the latest announcements without manually checking the site. This tool automates that process.

---

## Core Features

* **Serverless**: Designed to run on-demand in a cloud environment, ensuring cost-effectiveness with no servers to manage.
* **Modular Design**: Easily extendable to monitor new websites. Each site is handled by its own self-contained parser.
* **Telegram Integration**: Pushes new articles or announcements directly to a Telegram chat or channel of your choice.
* **Stateful Notifications**: Keeps track of previously sent articles to avoid sending duplicate notifications.

---

## Conceptual Architecture

The system is designed to follow a simple, event-driven workflow:

1.  **Scheduled Trigger**: A scheduler (like a cron job) periodically invokes the main function.
2.  **Execution**: The serverless function runs and iterates through a list of target websites.
3.  **Parsing**: For each target, a dedicated parser module is called to fetch and extract new items (e.g., titles and links).
4.  **Filtering**: The results are compared against a stored history to identify only the new items.
5.  **Notification**: A formatted message with the new items is sent to the configured Telegram channel.
6.  **State Update**: The history is updated with the latest sent items, ready for the next run.

---

## Technology

This project is built primarily for **Google Cloud Platform (GCP)**, leveraging its managed serverless components. The simple core architectur can be easily adapted to other cloud providers (e.g., AWS Lambda, Azure Functions).

* **Primary Platform**: **Google Cloud Platform (GCP)**
* **Compute**: **Google Cloud Functions** for serverless, on-demand code execution.
* **Scheduling**: **Google Cloud Scheduler** to trigger the function on a regular, cron-like basis.
* **State Management**: **Cloud Storage** to persist the state and track sent articles.
* **Language**: **Python**
* **Core Logic**: Standard libraries for HTTP requests, HTML parsing, and interacting with the Telegram Bot API.

---

## Configuration

To run this script, you will need to provide as environment variables, for example:

* **`TELEGRAM_BOT_TOKEN`**: The API token for your Telegram bot.
* **`TELEGRAM_CHAT_ID`**: The unique identifier for the target Telegram chat or channel.

---

## Adding a New Website

The architecture is designed to make adding new websites simple. This will be achieved by:

1.  **Creating a Parser Module**: Writing a small, standalone script for the new website.
2.  **Defining the Logic**: This script's sole responsibility is to fetch the site's content and return a list of news items in a standardized format (e.g., a list of objects, each with a title and a link).
3.  **Registering the Module**: Adding the new parser to a central list that the main function processes during each run.

This approach ensures that the logic for each website is isolated, making the project easy to maintain and extend.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for more details.
