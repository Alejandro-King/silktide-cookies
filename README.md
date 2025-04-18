Consent Manager Installation Instructions

1. Extract the contents of this zip file
2. Place the files in your website directory
3. Add the following code to your HTML page, inside the <head> tag:

<link rel="stylesheet" id="silktide-consent-manager-css" href="path-to-css/silktide-consent-manager.css">
<script src="path-to-js/silktide-consent-manager.js"></script>
<script>
silktideCookieBannerManager.updateCookieBannerConfig({
  background: {
    showBackground: true
  },
  cookieIcon: {
    position: "bottomLeft"
  },
  cookieTypes: [
    {
      id: "notwendig",
      name: "Notwendig",
      description: "<p>Diese Cookies sind für das einwandfreie Funktionieren der Website erforderlich und können nicht deaktiviert werden. Sie helfen bei Funktionen wie dem Einloggen und dem Speichern Ihrer Datenschutzeinstellungen.</p>",
      required: true,
      onAccept: function() {
        console.log('Add logic for the required Notwendig here');
      }
    },
    {
      id: "statistik",
      name: "Statistik",
      description: "<p>Diese Cookies helfen uns, die Website zu verbessern, indem sie verfolgen, welche Seiten am beliebtesten sind und wie sich Besucher auf der Website bewegen.</p>",
      required: false,
      onAccept: function() {
        gtag('consent', 'update', {
          analytics_storage: 'granted',
        });
        dataLayer.push({
          'event': 'consent_accepted_statistik',
        });
      },
      onReject: function() {
        gtag('consent', 'update', {
          analytics_storage: 'denied',
        });
      }
    },
    {
      id: "marketing",
      name: "Marketing",
      description: "<p>Diese Cookies bieten zusätzliche Funktionen und Personalisierungen, um Ihre Erfahrung zu verbessern. Sie können von uns oder von Partnern gesetzt werden, deren Dienste wir nutzen.</p>",
      required: false,
      onAccept: function() {
        gtag('consent', 'update', {
          ad_storage: 'granted',
          ad_user_data: 'granted',
          ad_personalization: 'granted',
        });
        dataLayer.push({
          'event': 'consent_accepted_marketing',
        });
      },
      onReject: function() {
        gtag('consent', 'update', {
          ad_storage: 'denied',
          ad_user_data: 'denied',
          ad_personalization: 'denied',
        });
      }
    }
  ],
  text: {
    banner: {
      description: "<p>Wir verwenden auf unserer Website Cookies, um Ihre Benutzererfahrung zu verbessern, personalisierte Inhalte bereitzustellen und unseren Verkehr zu analysieren.&nbsp;<a href=\"https://your-website.com/cookie-policy\" target=\"_blank\">Cookie-Richtlinie.</a></p>",
      acceptAllButtonText: "Alle akzeptieren",
      acceptAllButtonAccessibleLabel: "Alle Cookies akzeptieren",
      rejectNonEssentialButtonText: "Nicht notwendige ablehnen",
      rejectNonEssentialButtonAccessibleLabel: "Nicht notwendige ablehnen",
      preferencesButtonText: "Einstellungen",
      preferencesButtonAccessibleLabel: "Einstellungen umschalten"
    },
    preferences: {
      title: "Passen Sie Ihre Cookie-Einstellungen an",
      description: "<p>Wir respektieren Ihr Recht auf Privatsphäre. Sie können wählen, einige Cookie-Typen nicht zu erlauben. Ihre Cookie-Einstellungen gelten für unsere gesamte Website.</p>",
      creditLinkText: "Holen Sie sich dieses Banner kostenlos",
      creditLinkAccessibleLabel: "Dieses Banner kostenlos erhalten"
    }
  },
  position: {
    banner: "bottomLeft"
  }
});
</script>
