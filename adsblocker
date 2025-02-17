/*
 * YouTube & Google Ads Blocker for Surge
 * Blocks ads and tracking by modifying API responses
 */

const body = JSON.parse($response.body);

// Remove ad-related fields
const adKeys = ["adPlacements", "playerAds", "promotions", "adBreaks", "ads", "adParams"];
for (let key of adKeys) {
    if (body[key]) {
        body[key] = [];
    }
}

// Remove ads from `playerResponse`
if (body.playerResponse) {
    ["adPlacements", "playerAds"].forEach(key => {
        if (body.playerResponse[key]) {
            body.playerResponse[key] = [];
        }
    });
}

// Remove ads from `nextResponse`
if (body.nextResponse) {
    ["adPlacements", "ads"].forEach(key => {
        if (body.nextResponse[key]) {
            body.nextResponse[key] = [];
        }
    });
}

// Remove YouTube ad tracking stats
if (body.responseContext && body.responseContext.serviceTrackingParams) {
    body.responseContext.serviceTrackingParams = body.responseContext.serviceTrackingParams.filter(
        param => !param.hasOwnProperty("ads")
    );
}

// Remove SuggestQueries (possible ad suggestions)
if (body.contents && body.contents.suggestQueries) {
    body.contents.suggestQueries = [];
}

// Modify response to remove ads & tracking
$done({ body: JSON.stringify(body) });
